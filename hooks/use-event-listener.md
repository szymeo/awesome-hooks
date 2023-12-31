# useEventListener

Hook for subscribing to browser events.

```typescript tsx
import {useEffect, useRef} from 'react';

export const useEventListener = <T extends HTMLElement = HTMLDivElement>(
    eventName: keyof WindowEventMap,
    handler: (event: Event) => void,
    element?: T | null,
) => {
    const savedHandler = useRef<(event: Event) => void>();

    useEffect(() => {
        savedHandler.current = handler;
    }, [handler]);

    useEffect(() => {
        const targetElement: T | Window = element || window;
        if (!(targetElement && targetElement.addEventListener)) {
            return;
        }

        const eventListener = (event: Event) => savedHandler.current?.(event);
        targetElement.addEventListener(eventName, eventListener);

        return () => {
            targetElement.removeEventListener(eventName, eventListener);
        };
    }, [eventName, element]);
};
```

Usage:

```typescript tsx
useEventListener('click', () => console.log('clicked'));
```

### Authors

[![szymeo](https://avatars.githubusercontent.com/u/11583029?v=4&s=40)](https://github.com/szymeo)