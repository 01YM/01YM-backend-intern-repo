## 4.2 Reflection

### What makes a good variable or function name?
- its clear, specific and easy to understand. For example the variable IsInWater is self explanitory. 

### What issues can arise from poorly named variables?
- Reader needs to look through way more code to understand what variables or functions do. Purpose of code might be misunderstood, this could lead to mistakes, bugs and wasted time. Its also going to be hard to debug.

### How did refactoring improve code readability?
- Replacing the vague naming with self explanitory one made the code clear and easy to understand 


## Messy Code 
- TThe code is taken from one of my previous projects. This version is difficult to understand because the function name and variable names are too short and unclear. A reader would not know what a, b, c, d, e, f, or UW() mean without searching through the rest of the code.


```csharp
void EW()
{
    a = true;
    b = false;
    rb.gravityScale = c;
    rb.linearDamping = d;

    if (animator)
    {
        animator.SetBool(e, false);
        animator.SetBool(f, true);
    }

    UW();
}
``` 
## Clean Code
- This version is easier to understand because the function and variable names clearly explain what is happening. A reader can quickly see that the player is entering water, flight is being disabled, water settings are applied, and the water surface is updated.

```csharp
void EnterWater()
{
    isInWater = true;
    isFlying = false;

    rb.gravityScale = waterGravityScale;
    rb.linearDamping = waterLinearDamping;

    if (animator)
    {
        animator.SetBool(IsFlyingHash, false);
        animator.SetBool(IsInWaterHash, true);
    }

    UpdateWaterSurface();
}
```