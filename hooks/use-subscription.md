# useSubscription

Hook for subscribing to an RxJS observable.

```typescript tsx
import {Observable} from 'rxjs';
import {useEffect, useRef} from 'react';

export const useSubscription = <T>(observable: Observable<T>, callback: (value: T) => void) => {
    const callbackRef = useRef(callback);
    callbackRef.current = callback;

    useEffect(() => {
        const subscription = observable.subscribe(callbackRef.current);
        return () => subscription.unsubscribe();
    }, [observable]);
}
```

Usage:

```typescript tsx
const interval$ = useSubscription(interval(1000), (value) => console.log(value));
```

### Authors

[![szymeo](https://avatars.githubusercontent.com/u/11583029?v=4&s=40)](https://github.com/szymeo)