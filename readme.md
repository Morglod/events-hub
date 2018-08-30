# events-hub

## Install

```
npm i @morglod/events-hub
```

## Example

```ts
type ExampleEventTypes = {
    newTasks: {
        tasks: {
            uuid: string,
            name: string,
        }[],
    },
    updateTasks: {
        tasks: {
            [uuid: string]: {
                name?: string,
            }
        }
    },
};

class ExampleHandler {
    handleEventTypes: (keyof ExampleEventTypes)[] = [ 'newTasks', 'updateTasks' ];
    handleEvent: HandlerFunc<ExampleEventTypes, 'newTasks'|'updateTasks'> = (event) => {
        if (event.type ==='newTasks') {

        }
    }
}

const exampleHub = new EventHub<ExampleEventTypes>([
    new ExampleHandler,
]);

exampleHub.emit({
    type: 'newTasks',
    payload: { tasks: [] },
});
```