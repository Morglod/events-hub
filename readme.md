# ts-event-hub

OOP oriented, fully typed, event hub

## Install

```
npm i https://github.com/Morglod/ts-event-hub.git
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

class ExampleHandler extends EventHandler<ExampleEventTypes, 'newTasks'> {
    constructor() {
        super([ 'newTasks' ], (event) => {
            if (event.type === 'newTasks') {
                console.log('Changed task uuids: ', event.payload.tasks.map(t => t.uuid).join(', '));
            }
        });
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