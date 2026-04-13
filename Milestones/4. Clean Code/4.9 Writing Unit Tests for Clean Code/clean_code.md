## Reflection 

### How do unit tests help keep code clean?
- The methods are smaller and more focused. When code is easy to test, it is easier to read, reuse, and maintain. refactoring also becomes safer because they quickly show whether the original behavior still works after code changes. This helps improve the structure without breaking important features.

### What issues did you find while testing?
- Edge cases can easily be missed without unit tests. For example, health could go below zero if the damage is larger than the current health. Ive also discovered that that damage logic is easier to verify when it is separated from animation and Unity-specific behavior. This made the code simpler and more reliable.

## Tests for EnemyHealth 

```csharp 
public static class DamageCalculator
{
    public static int ApplyDamage(int currentHp, int damage)
    {
        int newHp = currentHp - damage;
        return newHp < 0 ? 0 : newHp;
    }
}

using NUnit.Framework;

[TestFixture]
public class DamageCalculatorTests
{
    [Test]
    public void ApplyDamage_ReducesHealthCorrectly()
    {
        int result = DamageCalculator.ApplyDamage(10, 3);
        Assert.AreEqual(7, result);
    }

    [Test]
    public void ApplyDamage_HealthDoesNotGoBelowZero()
    {
        int result = DamageCalculator.ApplyDamage(2, 5);
        Assert.AreEqual(0, result);
    }

    [Test]
    public void ApplyDamage_ZeroDamageKeepsSameHealth()
    {
        int result = DamageCalculator.ApplyDamage(8, 0);
        Assert.AreEqual(8, result);
    }
}

```
