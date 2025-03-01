---
title: "Lily Game Engine"
date: true
draft: false
ShowBreadCrumbs: true
url: "/projects/lily"
description: "Game Engine in C++"
summary: ""
tags: []
ShowReadingTime: true
ShowWordCount: true
---

## Introduction

Lily is a custom game engine built from scratch using C++ and OpenGL. The engine features a modular architecture with core systems for rendering, physics, audio, and scripting. This project demonstrates modern game engine architecture and real-time rendering techniques.

## Core Features

- Entity Component System (ECS) architecture
- OpenGL-based rendering system
- Custom physics engine
- Audio system
- Scene management
- Resource management
- Event system

## Implementation Details

### Core Engine Architecture
```cpp
class LilyEngine {
public:
    static LilyEngine& Get() {
        static LilyEngine instance;
        return instance;
    }

    void Init();
    void Run();
    void Shutdown();

    Window& GetWindow() { return *m_Window; }
    Renderer& GetRenderer() { return *m_Renderer; }
    SceneManager& GetSceneManager() { return *m_SceneManager; }

private:
    LilyEngine() = default;
    
    std::unique_ptr<Window> m_Window;
    std::unique_ptr<Renderer> m_Renderer;
    std::unique_ptr<SceneManager> m_SceneManager;
    std::unique_ptr<ResourceManager> m_ResourceManager;
};
```

### Entity Component System
```cpp
class Entity {
public:
    Entity() = default;
    Entity(const Entity& other) = default;

    template<typename T, typename... Args>
    T& AddComponent(Args&&... args) {
        T& component = m_Scene->m_Registry.emplace<T>(m_EntityHandle, std::forward<Args>(args)...);
        return component;
    }

    template<typename T>
    T& GetComponent() {
        return m_Scene->m_Registry.get<T>(m_EntityHandle);
    }

    template<typename T>
    bool HasComponent() {
        return m_Scene->m_Registry.has<T>(m_EntityHandle);
    }

private:
    entt::entity m_EntityHandle{entt::null};
    Scene* m_Scene = nullptr;
};
```

### Rendering System
```cpp
class Renderer {
public:
    void Init();
    void BeginScene(const Camera& camera);
    void EndScene();
    
    void Submit(const std::shared_ptr<VertexArray>& vertexArray, 
                const std::shared_ptr<Shader>& shader,
                const glm::mat4& transform = glm::mat4(1.0f));

private:
    struct SceneData {
        glm::mat4 ViewProjectionMatrix;
    };
    std::unique_ptr<SceneData> m_SceneData;
};

class Shader {
public:
    Shader(const std::string& vertexSrc, const std::string& fragmentSrc);
    ~Shader();

    void Bind() const;
    void Unbind() const;

    void SetInt(const std::string& name, int value);
    void SetFloat(const std::string& name, float value);
    void SetFloat3(const std::string& name, const glm::vec3& value);
    void SetFloat4(const std::string& name, const glm::vec4& value);
    void SetMat4(const std::string& name, const glm::mat4& value);

private:
    uint32_t m_RendererID;
};
```

### Event System
```cpp
class Event {
public:
    enum class Type {
        None = 0,
        WindowClose, WindowResize, WindowFocus, WindowLostFocus, WindowMoved,
        KeyPressed, KeyReleased, KeyTyped,
        MouseButtonPressed, MouseButtonReleased, MouseMoved, MouseScrolled
    };

    virtual Type GetEventType() const = 0;
    virtual const char* GetName() const = 0;
    virtual std::string ToString() const { return GetName(); }

    bool Handled = false;
};

class EventDispatcher {
public:
    EventDispatcher(Event& event) : m_Event(event) {}

    template<typename T, typename F>
    bool Dispatch(const F& func) {
        if (m_Event.GetEventType() == T::GetStaticType()) {
            m_Event.Handled |= func(static_cast<T&>(m_Event));
            return true;
        }
        return false;
    }

private:
    Event& m_Event;
};
```

## Technical Features

### Graphics
- Modern OpenGL rendering pipeline
- PBR (Physically Based Rendering) materials
- Dynamic lighting system
- Custom shader system
- Texture and material management
- Post-processing effects

### Physics
- Rigid body dynamics
- Collision detection and resolution
- Physics material system
- Ray casting
- Trigger volumes

### Audio
- 3D spatial audio
- Audio effect processing
- Stream management
- Multiple audio source support

### Tools
- Scene editor
- Material editor
- Asset management system
- Profiling tools
- Debug visualization

## Future Development

1. Vulkan rendering backend
2. Advanced animation system
3. Particle system
4. Network multiplayer support
5. Visual scripting system
6. Asset streaming system

## Resources

Check out the code: [Lily Engine on GitHub](https://github.com/kanand003/Lily)

### Learning Resources
- [Game Engine Series by The Cherno](https://www.youtube.com/playlist?list=PLlrATfBNZ98dC-V-N3m0Go4deliWHPFwT) - An excellent tutorial series on building a game engine from scratch
- [OpenGL Tutorial Series by The Cherno](https://www.youtube.com/playlist?list=PLlrATfBNZ98foTJPJ_Ev03o2oq3-GGOS2) - Modern OpenGL tutorials that helped with the rendering system implementation

<!--Add photo -->