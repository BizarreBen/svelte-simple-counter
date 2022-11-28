# svelte-simple-counter

:warning: **Currently not compatible with Firefox and Safari**

A simple animated numeric counter based on css @property

## Usage

```tsx
import { SimpleCounter } from 'svelte-simple-counter';

<SimpleCounter
	value={value}
	delay={delay}
	transitionDuration={duration}
	transitionTiming={timing}
/>;
```

### Configuration options

| Name               | Type   | Description                                                                    |
| ------------------ | ------ | ------------------------------------------------------------------------------ |
| value              | number | **Required** - displayed variable number                                       |
| delay              | number | animation start delay in milliseconds - defaults to 100                        |
| transitionDuration | number | duration in milliseconds of the transition on number change - defaults to 1000 |
| transitionTiming   | string | transition css timing function - defaults to 'ease'                            |
