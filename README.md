# UnityChaosList
Common faults i found while using Unity


## Unity is not Thread-Safe
You cannot call GUI-Elements or even other Unity internal related functions from another thread.<br>
If you do that, Unity will NOT give you an error, it will implode in itself silently.<br>
Your Monobehaviour-Script will just stop executing but not stop running. Like a zombie, it will remain.<br>
Thats why there is no error, it did not technically fail.. it just locks up.

## Either Monobehaviour or not
If you intent to use inheritence, good luck.<br>
As C# does not allow multible class-inheritence and Monobehaviour blocks the only one, you are required to make chain-inheritence.<br>
Classes that do not use Monobehavior can be used as normal, its really just a smal inconvinience but still.


## MONO does not like beeing told that stuff is UTF-8 

```CS
string myString = new string(myStringBuffer, 0, myStringBufferLength, System.Text.Encoding.UTF8);	
```
The fix is to just not tell. Otherwise it will fail internally while parsing the buffer.
```CS
string myString = new string(myStringBuffer, 0, myStringBufferLength);	
```

## Unity - UWP / Hololens is can't use directly pinned memory.
> Reference rewriter: Error: method `System.Char& modreq(System.Runtime.InteropServices.InAttribute) System.String::GetPinnableReference()` doesn't exist in target framework

```CS
fixed(char* myStringAdress = myString)
{
  // Do stuff
}		
```

The fix is solved by adding "ToCharArray()" to the string instead of letting the language handle the problem.<br>
There seems to be a hidden function call that does not exists in this older version.

```CS
fixed(char* myStringAdress = myString.ToCharArray())
{
  // Do stuff
}		
```
