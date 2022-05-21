# Bloc

Bloc est un solution de gestion state management. Ses concurrents sont:
- RxDart
- Redux
- Provider
- yolo
- test

Bloc veut dire: <b>B</>usiness <b>Lo</>gic <b>C</>omponent
<br>
Cela signifie que l'on va séparé le `business logic` de la `presentation` et des `data`

```
├── business logic  (`lib/xxxxx/bloc`)
├── data            (`/packages`)
├── presentation    (`lib/xxxxx/view`)
``` 
On peut faire conserver une structure plus simple en mettant tout dans `lib/xxxxx/`

## Structure de Bloc: `lib/xxxxx/bloc`
```
└── bloc
    ├── object_bloc.dart
    ├── object_event.dart
    ├── object_state.dart
```
// TODO finir l'explication ici


## Implementation dans la presentation: `lib/xxxxx/view`

      Widget build(BuildContext context) {
        return Container(

          child: RepositoryProvider.value(  <= Super important de l'avoir si on doit connecter un repository

            value: ObjectRepository(),

            child: BlocProvider<ObjectBloc>(

                create: (BuildContext context) => ObjectBloc(registerRepository: RepositoryProvider.of<ObjectRepository>(context)),
                
                child: BlocBuilder<ObjectBloc, ObjectState>( <= Important de ne pas oublier les <ObjectBloc, ObjectState>

                    builder: (context, state) {

                      return ElevatedButton(
                          child: const Text('click me'),
                          onPressed:  () {
                            context.read<ObjectBloc>().add(const EventBlocClicked());
                          },
                        );
                    }
                )
            ),
          ),
        );
     }
