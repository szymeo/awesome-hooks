# useSubscriptionState

Hook for setting state from an RxJS observable.

```typescript
import {Observable} from 'rxjs';
import {DependencyList, useEffect} from 'react';

export const useSubscriptionState = <T>(observable: Observable<T>, deps: DependencyList, initialState = null) => {
    const [state, setState] = useState(initialState);

    // useSubscription can be utilised here
    useEffect(() => {
        const subscription = observable.subscribe(setState);
        return () => subscription.unsubscribe();
    }, deps);

    return state;
}
```

Usage:

```typescript jsx
const time = useSubscriptionState(interval(1000), [], 0);

return (
    <p>{time}</p>
);
```

### Authors

[![szymeo](https://avatars.githubusercontent.com/u/11583029?v=4&s=40)](https://github.com/szymeo)