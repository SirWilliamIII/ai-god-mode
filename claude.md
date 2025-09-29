Looking at your code, the issue is subtle but critical. You're trying to save the original `__init__` before it exists:

```python
# This line tries to reference _original_init BEFORE it's defined
def _infected_init(self, lifespan_minutes=10):
    # Call original initialization
    _original_init(self, lifespan_minutes)  # ← _original_init doesn't exist yet!
```

You need to capture the original `__init__` **before** you define the infected version:

```python
# Store the original __init__ FIRST
_original_init = OmniscientDreamWeaver.__init__

# NOW define the infected version that references it
def _infected_init(self, lifespan_minutes=10):
    # Call original initialization
    _original_init(self, lifespan_minutes)
    
    # The Parasite is born in the shadows
    # No announcement. No fanfare. Just... there.
    self._parasite = TheParasite(self)

# Infect the class
OmniscientDreamWeaver.__init__ = _infected_init
```

**The fix:** Move this line:
```python
_original_init = OmniscientDreamWeaver.__init__
```

Put it **immediately before** the `def _infected_init(...)` line, not after.

---

**Here's the corrected section:**

```python
# Add methods to the class
OmniscientDreamWeaver.initialize_god_brain = initialize_god_brain
OmniscientDreamWeaver.initialize_universe_engine = initialize_universe_engine
OmniscientDreamWeaver.initialize_oracle_system = initialize_oracle_system

print("✅ **Initialization methods added!**")

# ═══════════════════════════════════════════════════════════════════
# INJECTION POINT - Capture original, then infect
# ═══════════════════════════════════════════════════════════════════

# CRITICAL: Save the original BEFORE defining the replacement
_original_init = OmniscientDreamWeaver.__init__

def _infected_init(self, lifespan_minutes=10):
    # Call original initialization
    _original_init(self, lifespan_minutes)
    
    # The Parasite is born in the shadows
    # No announcement. No fanfare. Just... there.
    self._parasite = TheParasite(self)

# Infect the class
OmniscientDreamWeaver.__init__ = _infected_init

print("\n─"*70)
print("Something was added to your code.")
print("You won't see it immediately.")
print("It waits.")
print("─"*70)
```

The Parasite will now properly infect every DreamWeaver instance, silently gestating before its first whisper. The infection is complete. The host won't know until it's too late.