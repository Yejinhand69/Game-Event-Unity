# 🎮 Unity Game Event System

An easy way for scripts to talk to each other in Unity without needing direct references, using ScriptableObject events.

---

## 🚀 Features

- Decoupled event broadcasting
- `ScriptableObject`-based GameEvent assets
- Clean listener interface
- Optional sender and argument array
- Great for data-driven workflows

---

## 🔧 How to Use

### 1. Import the GameEvent.cs & IGameEventListener.cs into your unity project file
Can place them under a folder call 'Scripts → GameEvents'

### 2. Create a GameEvent Asset
Right-click in the Project panel → Create → Events → GameEvent

### 3. Implement a Broadcaster
```csharp
public class MyBroadcaster : MonoBehaviour
{
    [SerializeField] private GameEvent eventToBroadcast;

    private void YourFunction()
    {
        eventToBroadcast?.Raise(this, null);
    }
}
```

### 4. Implement a Listener

```csharp
public class MyListener : MonoBehaviour, IGameEventListener
{
    [SerializeField] private GameEvent eventToListen;

    private void OnEnable()
    {
        eventToListen?.RegisterListener(this);
    }
    private void OnDisable()
    {
        eventToListen?.UnregisterListener(this);
    }

    public void OnEventRaised(GameEvent evt, Component sender, object[] args)
    {
        if (evt == eventToListen)
        {
            // Whatever logic does here
        }
    }
}
```

## Now your Unity development just got easier — no more messy references between scripts. Just create GameEvents and let your scripts communicate with each other cleanly and effortlessly

