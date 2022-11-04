# UnityChaosList
Common faults i found while using Unity


## Unity is not Thread-Safe
You cannot call GUI or even other Unity internal related functions.<br>
If you do that, Unity will NOT give you an error, it will fail silently.

## Monobehavior, the performence ancer
If you intent to use inheritence, good luck.<br>
As C# does not allow multible classes and Monobehaviour blocks the only one other one you are required to make chain-inheritence.<br>
Classes that do not use Monobehavior can be used as normal, its really just a smal inconvinience but still.
