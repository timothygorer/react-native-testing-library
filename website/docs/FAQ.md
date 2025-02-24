---
id: faq
title: FAQ
---

<details>
  <summary>Can I test native features of React Native apps?</summary>

<br />
<p>Short answer: no.</p>

React Native Testing Library does not provide a full React Native runtime since that would require running on physical device
or iOS simulator/Android emulator to provision the underlying OS and platform APIs.

Instead of using React Native renderer, it simulates only the JavaScript part of its runtime by 
using [React Test Renderer](https://reactjs.org/docs/test-renderer.html) while providing queries
and `fireEvent` APIs that mimick certain behaviors from the real runtime.

This approach has certain benefits and shortfalls. On the positive side:

- it allows testing most of the logic of regular React Native apps
- it allows running test on any OS supported by Jest, or other test runner, e.g. on CI
- it uses much less resources than full runtime simulation
- you can use Jest fake timers

The the negative side:

- you cannot test native features
- certain JavaScript features might not be perfectly simulated, but we are working on it

For instance, [react-native's ScrollView](https://reactnative.dev/docs/scrollview) has several props that depend on native calls. While you can trigger `onScroll` call with `fireEvent.scroll`, `onMomentumScrollBegin` is called from the native side and will therefore not be called.

</details>
