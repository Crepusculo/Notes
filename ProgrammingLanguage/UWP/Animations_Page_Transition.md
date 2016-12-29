http://stackoverflow.com/questions/32579445/uwp-page-transition-animations

```csharp
protected virtual void SetUpPageAnimation()
{
    TransitionCollection collection = new TransitionCollection();
    NavigationThemeTransition theme = new NavigationThemeTransition();

    var info = new ContinuumNavigationTransitionInfo();

    theme.DefaultNavigationTransitionInfo = info;
    collection.Add(theme);
    this.Transitions = collection;
}
```

`DefaultNavigationTransitionInfo() `
`ContinuumNavigationTransitionInfo()`
`CommonNavigationTransitionInfo()`
`DrillInNavigationTransitionInfo()`
`EntranceNavigationTransitionInfo()`
`SuppressNavigationTransitionInfo()`
`SlideNavigationTransitionInfo()`
