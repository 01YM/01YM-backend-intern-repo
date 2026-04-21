## 4.8 Reflection 
### What code smells did you find in your code?
The main code smells I found in the original EnemyHealth script were magic numbers, magic strings, and a method doing too many responsibilities. Some animation names were written directly as strings. The variable name hp was also less clear than a more descriptive name like currentHP. The TakeDamage() method handled at least six different things all in one method.

### How did refactoring improve the readability and maintainability of the code?
- separating the logic into smaller helper methods made the code easier to read because each method now has one clear responsibility. Replacing hardcoded strings and numbers with named constants and variables also made the code more descriptive and safer to edit later. Renaming variables like hp to currentHP and anim to animator made the script clearer for other developers.

### How can avoiding code smells make future debugging easier?
- code becomes more organized and predictable. When logic is split into smaller methods, it is easier to test and find where a bug happens. For example, if there is a problem with death handling, it can be checked inside HandleDeath() without searching through the whole TakeDamage() method. Using constants also reduces mistakes caused by misspelled animation strings or forgotten hardcoded values. 

## Messy code 
- Took this script from one of my previous projects. This EnemyHealth script manages enemy health, damage, stun effects, and death. 
```csharp 

[RequireComponent(typeof(Animator))]
public class EnemyHealth : MonoBehaviour, IDamageable
{
    public int maxHP = 3;
    public float stunTime = 0.35f;

    int hp;
    Animator anim;
    bool dead;

    void Awake() { hp = maxHP; anim = GetComponent<Animator>(); }

    public void TakeDamage(int amount, Vector2 knockback)
    {
        if (dead) return;
        hp -= amount;
        anim.SetTrigger("Hit");
        if (hp <= 0)
        {
            dead = true;
            anim.SetTrigger("Die");
            // Optional: disable collisions so it falls through or stops interacting
            foreach (var c in GetComponents<Collider2D>()) c.enabled = false;
            Destroy(gameObject, 1.2f);
        }
        else
        {
            StartCoroutine(StunRoutine());
        }
    }

    System.Collections.IEnumerator StunRoutine()
    {
        anim.SetBool("IsStunned", true);
        yield return new WaitForSeconds(stunTime);
        anim.SetBool("IsStunned", false);
    }
}

```

## Clean code

```csharp 
using System.Collections;
using UnityEngine;

[RequireComponent(typeof(Animator))]
public class EnemyHealth : MonoBehaviour, IDamageable
{
    [Header("Health")]
    public int maxHP = 3;

    [Header("Effects")]
    public float stunTime = 0.35f;
    public float destroyDelay = 1.2f;

    private const string HitTrigger = "Hit";
    private const string DieTrigger = "Die";
    private const string IsStunnedBool = "IsStunned";

    private int currentHP;
    private Animator animator;
    private bool isDead;

    private void Awake()
    {
        currentHP = maxHP;
        animator = GetComponent<Animator>();
    }

    public void TakeDamage(int amount, Vector2 knockback)
    {
        if (isDead)
            return;

        ApplyDamage(amount);
        PlayHitAnimation();

        if (IsDead())
        {
            HandleDeath();
            return;
        }

        StartCoroutine(StunRoutine());
    }

    private void ApplyDamage(int amount)
    {
        currentHP -= amount;
    }

    private void PlayHitAnimation()
    {
        animator.SetTrigger(HitTrigger);
    }

    private bool IsDead()
    {
        return currentHP <= 0;
    }

    private void HandleDeath()
    {
        isDead = true;
        animator.SetTrigger(DieTrigger);
        DisableColliders();
        Destroy(gameObject, destroyDelay);
    }

    private void DisableColliders()
    {
        Collider2D[] colliders = GetComponents<Collider2D>();

        foreach (Collider2D collider in colliders)
        {
            collider.enabled = false;
        }
    }

    private IEnumerator StunRoutine()
    {
        animator.SetBool(IsStunnedBool, true);
        yield return new WaitForSeconds(stunTime);
        animator.SetBool(IsStunnedBool, false);
    }
}
```