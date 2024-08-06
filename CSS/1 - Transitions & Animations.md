## Transitions
Transitions wait until a change in a property occurs and then allows those changes to take place over time.
* Without a transition, any changes in a property will take effect immediately.
* Transitions should be used when properties are changed interactively. For example, when an element is hovered on.  

```
transition-property: transfor;
transition-duration: 0.3s;
transition-timing-function: ease | ease-in ...;
transition-delay: 0.3s;

.btn:hover {
transform: translateY(-10px)
}
```
* Transition property defines the property that the transition will target.

```
transition: transition-property transition-duration transition-timing-function transition-delay
```
* Shortcut that combines all the transition properties into one.
## Animations
Animations provide keyframes for more control over animations, which allows us to create complex animations on a frame by frame basis.
* Animations should be used to create animations that should happen without having to wait for properties that change interactively.
* Animations and transitions can be combined.