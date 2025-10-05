---
title: Inspector Button
author: <SW>
categories: [Unity]
tags: [Scripts]
media_subpath: /media/
---

# Unity Inspector Button



I really like the idea of customizing how a script is displayed in the Unity Inspector.  Bringing simplified functionality is a very satisfying endeavour.



Creating custom property drawers is one option. Creating custom inspector windows for each script is also an option.
However I found the prospect of creating custom property drawers for each custom data type to be an onerous task fraught with frustration, doubly so for custom inspector displays on a per script basis.
Even with inherited class structures it was often more trouble than they were worth unless you are delivering a final toolset specifically for artists.



Surely for rapidly prototyping amongst smaller teams there has to be a middle ground of some sort?



I discovered that there was.



It is possible to create a generic property drawer to suit this very purpose.


Normal script:

<img width="450" height="139" alt="image" src="https://github.com/user-attachments/assets/11531ea9-9695-40b6-b002-debb0f23bd5c" />

Script with a boolean property:

<img width="456" height="78" alt="image" src="https://github.com/user-attachments/assets/17751fb0-8521-4598-a697-b7b9410bc475" />

Boolean property replaced with a functional button: 

<img width="454" height="128" alt="image" src="https://github.com/user-attachments/assets/74f8b2e3-04ea-4414-8dd3-9221edce47c0" />



## General Idea

The general implementation is simple (I've included a copy of the script at the bottom of this post).

Any serializable attribute can be assigned a custom property drawer to draw a simple button and call a local function.

```
public class MyScript : MonoBehaviour
{
    [InspectorButton("DoMethod", "ButtonTitle")]
    public bool btnDO;
    
    public void DoMethod()
    {
        Debug.Log("PRESSED BUTTON");
    }
}
```

Instead of drawing the boolean attribute, we are shown a button instead.

There is a bit of flexibility regarding it's display and implementation.

The attribute you want to override should not be used in any other parts of the script.  It can still function as a regular property, but it's cleaner and easier to remove later if you stick to a consistent naming
and usage.  It is essentially 'throw-away'. And only used to act as a gui location for the button to be drawn in it's stead.

<img width="456" height="78" alt="image" src="https://github.com/user-attachments/assets/2eb1d12d-5e28-4ac0-bdf6-0eeace881c19" />

## Basic Usage

```
    [InspectorButton("DoMethod")]
    public bool btnDO;
```

<img width="452" height="77" alt="image" src="https://github.com/user-attachments/assets/984f8c30-15b7-4129-95b4-5bb007c20e2e" />

At minimum, you need to declare the local function it should call.

The button will display the name of the function.



## Custom Button Title

```
    [InspectorButton("DoMethod", "Button Title")]
    public bool btnDO;
```

<img width="453" height="76" alt="image" src="https://github.com/user-attachments/assets/eccfa561-2f63-4239-90ee-2298b3c39aee" />

You can also set the width and center point of the button if you need to make it fit a certain aesthetic.



### Syntax

```
InspectorButtonAttribute ( string MethodName, string ButtonTitle, float width, float center )
```




## Bulk Buttons!

Naturally the next issue that will arise is scalability.  You may want to have several buttons created in one place.  This could be for many different reasons.
Fortunately, you can also do an array of buttons in one shot.

<img width="454" height="73" alt="image" src="https://github.com/user-attachments/assets/add4b339-c339-46f4-ac45-f5690ad2728c" />

```
    [InspectorButton(new string[]{"DoMethod", "DoMethod2", "DoMethod3"}, new string[] { "Button Title", "Button 2", "Button 3" }, 100)]
    public bool btnDO;
```

This way we are not polluting our script with wrappers and decorators we only need temporarily.  Easy to add.  Easy to remove.




# InpsectorButton.cs

Here is the full InspectorButton.cs script for you to play with.

```
using UnityEngine;
#if UNITY_EDITOR
using UnityEditor;
#endif
using System.Reflection;

/// <summary>
/// This attribute can only be applied to fields because its
/// associated PropertyDrawer only operates on fields (either
/// public or tagged with the [SerializeField] attribute) in
/// the target MonoBehaviour.
/// </summary>
/// 

namespace SW
{
    [System.AttributeUsage(System.AttributeTargets.Field)]
    public class InspectorButtonAttribute : PropertyAttribute
    {
        public static float kDefaultButtonWidth = 80;

        public readonly string MethodName;
        public readonly string ButtonTitle;

        public readonly string[] MethodNameS;
        public readonly string[] ButtonTitleS;

        private float _buttonWidth = -1f;
        public float ButtonWidth
        {
            get { return _buttonWidth; }
            set { _buttonWidth = value; }
        }
        private float _buttonCenter = 1f;
        public float ButtonCenter
        {
            get { return _buttonCenter; }
            set { _buttonCenter = value; }
        }


        public InspectorButtonAttribute(string MethodName)
        {
            this.MethodName = MethodName;
            this.ButtonTitle = MethodName;

        }
        public InspectorButtonAttribute(string[] MethodNameS, string[] ButtonTitleS)
        {
            this.MethodNameS = MethodNameS;
            this.ButtonTitleS = ButtonTitleS;

        }
        public InspectorButtonAttribute(string[] MethodNameS, string[] ButtonTitleS, float width)
        {
            this.MethodNameS = MethodNameS;
            this.ButtonTitleS = ButtonTitleS;
            this.ButtonWidth = width;

        }
        public InspectorButtonAttribute(string MethodName, string ButtonTitle)
        {
            this.MethodName = MethodName;
            this.ButtonTitle = ButtonTitle;

        }
        public InspectorButtonAttribute(string MethodName, string ButtonTitle, float width)
        {
            this.MethodName = MethodName;
            this.ButtonTitle = ButtonTitle;
            this.ButtonWidth = width;

        }
        public InspectorButtonAttribute(string MethodName, string ButtonTitle, float width, float center)
        {
            this.MethodName = MethodName;
            this.ButtonTitle = ButtonTitle;
            this.ButtonWidth = width;
            this.ButtonCenter = center;
        }
    }

#if UNITY_EDITOR
    [CustomPropertyDrawer(typeof(InspectorButtonAttribute))]
    public class LS_InspectorButtonPropertyDrawer : PropertyDrawer
    {
        private MethodInfo _eventMethodInfo = null;
        private MethodInfo[] _eventMethodInfoS = null;

        public override void OnGUI(Rect position, SerializedProperty prop, GUIContent label)
        {
            InspectorButtonAttribute inspectorButtonAttribute = (InspectorButtonAttribute)attribute;

            label.text = inspectorButtonAttribute.ButtonTitle;
            GUIStyle style = GUI.skin.box;
            if (inspectorButtonAttribute.ButtonWidth == -1f)
            {
                inspectorButtonAttribute.ButtonWidth = style.CalcSize(label).x + 20f;
            }
            float leftPos = -position.x + (inspectorButtonAttribute.ButtonWidth) * 0.5f;
            float centerPos = position.x + (position.width - inspectorButtonAttribute.ButtonWidth) * 0.5f;
            float offsetPos = (leftPos * (1f - inspectorButtonAttribute.ButtonCenter)) + (centerPos * (inspectorButtonAttribute.ButtonCenter));
            Rect buttonRect = new Rect(offsetPos, position.y, inspectorButtonAttribute.ButtonWidth, position.height);

            if (inspectorButtonAttribute.MethodNameS == null || inspectorButtonAttribute.MethodNameS.Length == 0)
            {
                if (GUI.Button(buttonRect, label.text))
                {
                    System.Type eventOwnerType = prop.serializedObject.targetObject.GetType();
                    string eventName = inspectorButtonAttribute.MethodName;
                    string[] eventNameS = inspectorButtonAttribute.MethodNameS;

                    if (_eventMethodInfo == null)
                        _eventMethodInfo = eventOwnerType.GetMethod(eventName, BindingFlags.Instance | BindingFlags.Static | BindingFlags.Public | BindingFlags.NonPublic);

                    if (_eventMethodInfo != null)
                        _eventMethodInfo.Invoke(prop.serializedObject.targetObject, null);
                    else
                        Debug.LogWarning(string.Format("InspectorButton: Unable to find method {0} in {1}", eventName, eventOwnerType));
                }
            }
            else
            {
                int methodCount = inspectorButtonAttribute.MethodNameS.Length;
                Rect thisRect = buttonRect;

                for (int i = 0; i < methodCount; i++)
                {
                    thisRect.x = (buttonRect.width * i);
                    if (GUI.Button(thisRect, inspectorButtonAttribute.ButtonTitleS[i]))
                    {
                        System.Type eventOwnerType = prop.serializedObject.targetObject.GetType();
                        string eventName = inspectorButtonAttribute.MethodNameS[i];

                        _eventMethodInfo = eventOwnerType.GetMethod(inspectorButtonAttribute.MethodNameS[i], BindingFlags.Instance | BindingFlags.Static | BindingFlags.Public | BindingFlags.NonPublic);

                        if (_eventMethodInfo != null)
                        {
                            _eventMethodInfo.Invoke(prop.serializedObject.targetObject, null);
                        }
                        else
                            Debug.LogWarning(string.Format("InspectorButton: Unable to find method {0} in {1}", eventName, eventOwnerType));

                    }
                }
            }
        }
    }
#endif
}
```
