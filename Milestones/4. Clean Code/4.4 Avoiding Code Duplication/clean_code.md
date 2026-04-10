## 4.4 Reflection 

### What were the issues with duplicated code?
- One big issue I found is that if you need to change the duplicated parameter, youll need to go through the entire file and change it at every instance. It increases the chances of inconsistent code or behaivour. 

### How did refactoring improve maintainability?
- In my example, moving the SetVertiacalVelocity into a seperate function made it easy to update. 

## Messy code 
- This version repeats the same pattern for setting vertical velocity. The code works, but the repeated new Vector2(rb.linearVelocity.x, ...) makes it more repetitive and harder to maintain

```csharp
void Jump()
{
    rb.linearVelocity = new Vector2(rb.linearVelocity.x, jumpForce);
    if (animator) animator.SetTrigger(JumpHash);
}

void Flap()
{
    float newVy = rb.linearVelocity.y + flyImpulse;
    if (newVy > maxFlapUpSpeed) newVy = maxFlapUpSpeed;
    rb.linearVelocity = new Vector2(rb.linearVelocity.x, newVy);
}

void EnterFlight()
{
    isFlying = true;
    rb.gravityScale = flyGravityScale;
    rb.linearVelocity = new Vector2(rb.linearVelocity.x, Mathf.Min(rb.linearVelocity.y, 0f));
    if (animator) animator.SetBool(IsFlyingHash, true);
}
``` 
## Clean code 
- removing duplication by moving the repeated vertical velocity update into one helper function makes the code shorter and more consistent. We then just call the setverticalvelocity from other methods. 

```csharp 
void SetVerticalVelocity(float newY)
{
    rb.linearVelocity = new Vector2(rb.linearVelocity.x, newY);
}

void Jump()
{
    SetVerticalVelocity(jumpForce);

    if (animator)
        animator.SetTrigger(JumpHash);
}
``` 


