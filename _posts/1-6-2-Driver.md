---
layout: doc
permalink: /docs/ui-toolkit/animation/driver
title: Driver
section: Animation
---

# Driver

An animation is driven by the `driver`. It encapsulates the creation of animation [input events](https://facebook.github.io/react-native/docs/animations.html#input-events), making React Native animations even more declarative. Drivers are attached to animation components which are set to listen to specific driver inputs.

Currently, 2 drivers are supported:

- `ScrollDriver`, that binds scrolling of RN [ScrollView](https://facebook.github.io/react-native/docs/scrollview.html) to the attaching animation components and
- `TimingDriver`, that creates animated values changing with time


## ScrollDriver

Binding is done by passing properties to `ScrollView`:

```javascript
import React from 'react';
import { ScrollView } from 'react-native';
import { ScrollDriver } from '@shoutem/animation';


class Screen extends React.Component {
  render() {
    const driver = new ScrollDriver();

    return (
      <ScrollView {...driver.scrollViewProps}>
        {/* Pass driver to animation components */}
      </ScrollView>
    );
  }
}
```

## TimingDriver

Animated value is changing with time:

```javascript
import React from 'react';
import { View, Easing } from 'react-native';
import { TimingDriver, FadeIn } from '@shoutem/animation';

class Screen extends React.Component {
  render() {
    driver = new TimingDriver({
      duration: 400 // 250 by default,
      easing: Easing.inOut // Easing.cubic is passed by default
      delay: 200 // 0 by default
    });

    return (
      <View>
        <FadeIn driver={driver}>
          {/* Some components to fade in with time passing */}
        </FadeIn>
      </View>
    )
  }
}
```

To trigger the start of the timer, call `runTimer` method on `TimingDriver` instance. The signature of `runTimer` method is as follows:

#### `runTimer(endValue, onFinish)`: 

- `endValue`: Number, when the timer reaches this value the animations will end
- `onFinish` Function, callback that will be called upon reaching `endValue`
