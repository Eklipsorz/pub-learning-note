
若貿然使用以下

```
const inputRef = useRef();

  const activate = () => {
    inputRef.current.focus();
  };

  useImperativeHandle(ref, () => {
    console.log('test', typeof activate, '|', typeof inputRef.current.focus);
    return {
      focus: inputRef.current.focus,
    };
});
```

會顯示以下訊息


```
Login.js:106 Uncaught TypeError: Illegal invocation
    at submitHandler (Login.js:106:1)
    at HTMLUnknownElement.callCallback (react-dom.development.js:4164:1)
    at Object.invokeGuardedCallbackDev (react-dom.development.js:4213:1)
    at invokeGuardedCallback (react-dom.development.js:4277:1)
    at invokeGuardedCallbackAndCatchFirstError (react-dom.development.js:4291:1)
    at executeDispatch (react-dom.development.js:9041:1)
    at processDispatchQueueItemsInOrder (react-dom.development.js:9073:1)
    at processDispatchQueue (react-dom.development.js:9086:1)
    at dispatchEventsForPlugins (react-dom.development.js:9097:1)
    at react-dom.development.js:9288:1
    at batchedUpdates$1 (react-dom.development.js:26140:1)
    at batchedUpdates (react-dom.development.js:3991:1)
    at dispatchEventForPluginEventSystem (react-dom.development.js:9287:1)
    at dispatchEventWithEnableCapturePhaseSelectiveHydrationWithoutDiscreteEventReplay (react-dom.development.js:6465:1)
    at dispatchEvent (react-dom.development.js:6457:1)
    at dispatchDiscreteEvent (react-dom.development.js:6430:1)
```