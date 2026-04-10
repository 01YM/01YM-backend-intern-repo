## 4.7 Reflection

### What made the original code complex?
- One method was handling too many things at once. Physics, jump timing, gravity logic, movement state, animation updates... It was very hard to understand whats going on or make any changes. 

### How did refactoring improve it?
- Splitting it into multiple methods with clear titeles made it much easier to read and understand as well as modify per requirements. It reduced the chance of changing one thing and accidentaly breaking the whole method or introducing weird bugs.

## Messy code
- This is the main function for the dragon mover that ended up being way too complicated and hard to understand. Its responsible for too many different things and is hard to read.

```csharp
void Update()
{
    bool wasGrounded = grounded;
    grounded = IsGrounded();

    if (!wasGrounded && grounded)
    {
        jumpedSinceGround = false;
        animator?.ResetTrigger(JumpHash);
    }

    if (grounded) lastGroundedTime = coyoteTime; else lastGroundedTime -= Time.deltaTime;
    if (lastJumpPressedTime > 0f) lastJumpPressedTime -= Time.deltaTime;

    if (!_inWater && lastGroundedTime > 0f && lastJumpPressedTime > 0f && !isFlying && !hideHeld && !crawlHeld)
    {
        Jump();
        lastGroundedTime = 0f;
        lastJumpPressedTime = 0f;
        if (debugLogs) Debug.Log("Jump: buffered/coyote");
    }

    if (!_inWater && !jumpHeld && !isFlying && rb.linearVelocity.y > 0f)
        rb.linearVelocity = new Vector2(rb.linearVelocity.x, rb.linearVelocity.y * jumpCutMultiplier);

    if (sprite && Mathf.Abs(moveInput.x) > 0.01f)
        sprite.flipX = moveInput.x < 0f;

    if (_inWater)
    {
        rb.gravityScale = waterGravityScale;
    }
    else if (isFlying)
    {
        if (jumpHeld)
        {
            rb.gravityScale = glideGravityScale;
            if (rb.linearVelocity.y > 0f)
                rb.linearVelocity = new Vector2(rb.linearVelocity.x, 0f);
            if (rb.linearVelocity.y < maxGlideFallSpeed)
                rb.linearVelocity = new Vector2(rb.linearVelocity.x, maxGlideFallSpeed);
        }
        else
        {
            rb.gravityScale = flyGravityScale;
        }
    }
    else
    {
        rb.gravityScale = normalGravityScale;
    }

    if (!_inWater && grounded && isFlying)
    {
        isFlying = false;
        rb.gravityScale = normalGravityScale;
        animator?.SetBool(IsFlyingHash, false);
        if (debugLogs) Debug.Log("Flight: exited (grounded)");
    }

    bool moving = Mathf.Abs(moveInput.x) > 0.01f;
    bool down = moveInput.y < -0.5f;
    bool horiz = Mathf.Abs(moveInput.x) > 0.1f;

    hideHeld = down && !horiz;
    crawlHeld = down && horiz;
    bool running = runHeld && grounded && moving;

    if (animator)
    {
        animator.SetBool(IsGroundedHash, grounded && !_inWater);
        animator.SetBool(IsMovingHash, moving);
        animator.SetBool(IsRunningHash, running);
        animator.SetBool(IsCrawlingHash, !_inWater && crawlHeld);
        animator.SetBool(IsHidingHash, !_inWater && hideHeld);
        animator.SetFloat(SpeedHash, Mathf.Abs(rb.linearVelocity.x), 0.06f, Time.deltaTime);
        animator.SetFloat(VSpeedHash, rb.linearVelocity.y);
        animator.SetBool(IsInWaterHash, _inWater);
        animator.SetBool(IsAtSurfaceHash, _isAtSurface);

        int swimDir = 0;
        if (_inWater && !_isAtSurface)
        {
            if (moveInput.y > 0.1f) swimDir = 1;
            else if (moveInput.y < -0.1f) swimDir = -1;
        }
        animator.SetInteger(SwimDirHash, swimDir);

        if (kickPressed) { animator.SetTrigger("Kick"); kickPressed = false; }
        if (attackPressed) { animator.SetTrigger("Attack"); attackPressed = false; }
    }
}
```

## Clean Code
- 

```csharp
void Update()
{
    UpdateGroundState();
    UpdateJumpTimers();
    HandleBufferedJump();
    ApplyJumpCut();
    UpdateSpriteDirection();
    UpdateGravityState();
    ExitFlightIfGrounded();
    UpdateMovementState();
    UpdateAnimatorState();
}

void UpdateGroundState()
{
    bool wasGrounded = grounded;
    grounded = IsGrounded();

    if (!wasGrounded && grounded)
    {
        jumpedSinceGround = false;
        animator?.ResetTrigger(JumpHash);
    }
}

void UpdateJumpTimers()
{
    if (grounded)
        lastGroundedTime = coyoteTime;
    else
        lastGroundedTime -= Time.deltaTime;

    if (lastJumpPressedTime > 0f)
        lastJumpPressedTime -= Time.deltaTime;
}

void HandleBufferedJump()
{
    if (_inWater || isFlying || hideHeld || crawlHeld)
        return;

    if (lastGroundedTime > 0f && lastJumpPressedTime > 0f)
    {
        Jump();
        lastGroundedTime = 0f;
        lastJumpPressedTime = 0f;

        if (debugLogs)
            Debug.Log("Jump: buffered/coyote");
    }
}

void ApplyJumpCut()
{
    if (!_inWater && !jumpHeld && !isFlying && rb.linearVelocity.y > 0f)
    {
        rb.linearVelocity = new Vector2(
            rb.linearVelocity.x,
            rb.linearVelocity.y * jumpCutMultiplier
        );
    }
}

void UpdateSpriteDirection()
{
    if (sprite && Mathf.Abs(moveInput.x) > 0.01f)
        sprite.flipX = moveInput.x < 0f;
}

void UpdateGravityState()
{
    if (_inWater)
    {
        rb.gravityScale = waterGravityScale;
        return;
    }

    if (isFlying)
    {
        ApplyFlightGravity();
        return;
    }

    rb.gravityScale = normalGravityScale;
}

void ApplyFlightGravity()
{
    if (jumpHeld)
    {
        rb.gravityScale = glideGravityScale;

        if (rb.linearVelocity.y > 0f)
            rb.linearVelocity = new Vector2(rb.linearVelocity.x, 0f);

        if (rb.linearVelocity.y < maxGlideFallSpeed)
            rb.linearVelocity = new Vector2(rb.linearVelocity.x, maxGlideFallSpeed);
    }
    else
    {
        rb.gravityScale = flyGravityScale;
    }
}

void ExitFlightIfGrounded()
{
    if (!_inWater && grounded && isFlying)
    {
        isFlying = false;
        rb.gravityScale = normalGravityScale;
        animator?.SetBool(IsFlyingHash, false);

        if (debugLogs)
            Debug.Log("Flight: exited (grounded)");
    }
}

void UpdateMovementState()
{
    bool down = moveInput.y < -0.5f;
    bool horizontalInput = Mathf.Abs(moveInput.x) > 0.1f;

    hideHeld = down && !horizontalInput;
    crawlHeld = down && horizontalInput;
}

void UpdateAnimatorState()
{
    if (!animator)
        return;

    bool moving = Mathf.Abs(moveInput.x) > 0.01f;
    bool running = runHeld && grounded && moving;

    animator.SetBool(IsGroundedHash, grounded && !_inWater);
    animator.SetBool(IsMovingHash, moving);
    animator.SetBool(IsRunningHash, running);
    animator.SetBool(IsCrawlingHash, !_inWater && crawlHeld);
    animator.SetBool(IsHidingHash, !_inWater && hideHeld);
    animator.SetFloat(SpeedHash, Mathf.Abs(rb.linearVelocity.x), 0.06f, Time.deltaTime);
    animator.SetFloat(VSpeedHash, rb.linearVelocity.y);
    animator.SetBool(IsInWaterHash, _inWater);
    animator.SetBool(IsAtSurfaceHash, _isAtSurface);
    animator.SetInteger(SwimDirHash, GetSwimDirection());

    if (kickPressed)
    {
        animator.SetTrigger("Kick");
        kickPressed = false;
    }

    if (attackPressed)
    {
        animator.SetTrigger("Attack");
        attackPressed = false;
    }
}

int GetSwimDirection()
{
    if (!_inWater || _isAtSurface)
        return 0;

    if (moveInput.y > 0.1f)
        return 1;

    if (moveInput.y < -0.1f)
        return -1;

    return 0;
}
```