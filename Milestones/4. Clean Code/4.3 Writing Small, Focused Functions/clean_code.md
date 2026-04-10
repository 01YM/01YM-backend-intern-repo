## 4.3 Reflection 

### Why is breaking down functions beneficial?
- Breaking down code makes it really easy to navigate, fix, update and change parameters without having to change everything else in the function that wasnt relevant. Its also easy to read, understand and find different functions

### How did refactoring improve the structure of the code?
- it improved the structure. Code became easy to test, debug and update. If I want to change something in a single parameter, I wont need to change everything else with it. 


## Messy code Example
- This version mixes checking the ground, jumping, flapping, and entering flight into one function. It works, but it is harder to understand because several different actions are combined together.

```csharp
void HandleMovement()
{
    if (!groundCheck) return;

    bool grounded = Physics2D.OverlapCircle(
        groundCheck.position,
        groundRadius,
        groundLayer
    ) != null;

    if (grounded)
    {
        rb.linearVelocity = new Vector2(rb.linearVelocity.x, jumpForce);

        if (animator)
            animator.SetTrigger(JumpHash);
    }
    else if (isFlying)
    {
        float newVelocityY = rb.linearVelocity.y + flyImpulse;

        if (newVelocityY > maxFlapUpSpeed)
            newVelocityY = maxFlapUpSpeed;

        rb.linearVelocity = new Vector2(rb.linearVelocity.x, newVelocityY);
    }
    else
    {
        isFlying = true;
        rb.gravityScale = flyGravityScale;

        rb.linearVelocity = new Vector2(
            rb.linearVelocity.x,
            Mathf.Min(rb.linearVelocity.y, 0f)
        );

        if (animator)
            animator.SetBool(IsFlyingHash, true);
    }
}
```

## Clean Code 
- each function has only one responsibility. One function handles jumping, one handles flapping, one handles entering flight, and one checks if the dragon is grounded.

```csharp 
void Jump()
{
    rb.linearVelocity = new Vector2(rb.linearVelocity.x, jumpForce);

    if (animator)
        animator.SetTrigger(JumpHash);
}

void Flap()
{
    float newVelocityY = rb.linearVelocity.y + flyImpulse;

    if (newVelocityY > maxFlapUpSpeed)
        newVelocityY = maxFlapUpSpeed;

    rb.linearVelocity = new Vector2(rb.linearVelocity.x, newVelocityY);
}

void EnterFlight()
{
    isFlying = true;
    rb.gravityScale = flyGravityScale;

    rb.linearVelocity = new Vector2(
        rb.linearVelocity.x,
        Mathf.Min(rb.linearVelocity.y, 0f)
    );

    if (animator)
        animator.SetBool(IsFlyingHash, true);
}

bool IsGrounded()
{
    if (!groundCheck)
        return false;

    return Physics2D.OverlapCircle(
        groundCheck.position,
        groundRadius,
        groundLayer
    ) != null;
}
```
