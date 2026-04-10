## 4.6 Reflection

### What was the issue with the original code?
- The original code assumed EnterWater method will always be called in a correct situation. It does not check if the dragon is already in the water or if the water collider exists. It relies on the outside code to always correctly execute. 
### How does handling errors improve reliability?
- The code will fail in a controlled way instead of creating bad states. invalid input and output will be stopped by guard clauses before it spreads through. Bugs become easier to find and it reduces unexpected behaveior. 

## Messy code 
- Although this is a working version of the code, it does not protect itself against invalid states. For example, entering the water twice or without a water collider.

```csharp
void EnterWater()
{
    _inWater = true;
    isFlying = false;
    rb.gravityScale = waterGravityScale;
    rb.linearDamping = waterLinearDamping;

    if (animator)
    {
        animator.SetBool(IsFlyingHash, false);
        animator.SetBool(IsInWaterHash, true);
    }

    UpdateWaterSurface();

    if (debugLogs)
        Debug.Log("Entered water");
}
```
## Clean code
- This version adds guard clauses at the top. The function exits early if the dragon is already in water or if there is no valid water collider. This makes the function safer and easier to trust. 
```csharp
void EnterWater()
{
    if (_inWater)
        return;

    if (_waterCollider == null)
    {
        if (debugLogs)
            Debug.LogWarning("EnterWater called without a water collider.");
        return;
    }

    _inWater = true;
    isFlying = false;
    rb.gravityScale = waterGravityScale;
    rb.linearDamping = waterLinearDamping;

    if (animator)
    {
        animator.SetBool(IsFlyingHash, false);
        animator.SetBool(IsInWaterHash, true);
    }

    UpdateWaterSurface();

    if (debugLogs)
        Debug.Log("Entered water");
}
```