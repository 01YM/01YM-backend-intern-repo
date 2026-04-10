## 4.5 Reflection 

### When should you add comments?
- When its not as obvious what the code does from reading the code alone.

### When should you avoid comments and instead improve the code?
- whenever the comment just repeaets what the code says. In this case, cleaner code will be more useful than the comment. For example renaming "newVy" to "newVertiacalVelocity" would be more useful than a comment on what it is. 

## Messy code
- This code doesnt have any useful comments that explains what is happening in it

```csharp
void EnterWater()
{
    _inWater = true;
    isFlying = false; // cancel flight in water
    rb.gravityScale = waterGravityScale;
    rb.linearDamping = waterLinearDamping;

    if (animator)
    {
        animator.SetBool(IsFlyingHash, false);
        animator.SetBool(IsInWaterHash, true);
    }

    UpWSurf(); //update water surface

    if (debugLogs)
        Debug.Log("Entered water");
}
```
## Clean code
The messy code had one comment that repeated what the code already showed. The improved version explain why flight is disabled and why the water surface is updated, which gives useful information

```csharp
void EnterWater()
{
    _inWater = true;

    // stop flying when entering water
    // so swimming movement takes control
    isFlying = false;

    rb.gravityScale = waterGravityScale;
    rb.linearDamping = waterLinearDamping;

    if (animator)
    {
        animator.SetBool(IsFlyingHash, false);
        animator.SetBool(IsInWaterHash, true);
    }

    // Update swim height limit
    UpdateWaterSurface();

    if (debugLogs)
        Debug.Log("Entered water");
}
```