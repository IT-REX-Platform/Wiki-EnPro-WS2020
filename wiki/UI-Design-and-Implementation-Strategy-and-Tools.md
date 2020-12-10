## Strategic perspective

Everyone is a fullstack developer. This gives everyone insights in the entire project. That makes all developers flexible. This means the UI is developed in parallel to the backend. The UI will be functional in the beginning and become more detailed with time.

## Itegration perspective

We will try to export the stylesheets from the prototype and use the prototype as a reference point for the UI development. The UI elements have to be adjusted to make the export possible. The UI elements have to get names that can be used as classes in the style sheets. As a framework we will use Expo with the bare workflow. This enables us to target all plattforms with one codebase. We try to minimize dependencies on Expo to switch to React-Native if necessary. This is done by strictly separating bussiness logic from the UI. 

## Implementation perspective

We use centrally defined style sheets for UI elements and don't change them without consulting the other developers. Those style sheets are exported from the prototype if possible. Otherwise they are created by us in advance. The style sheets are continuously maintained. Expo/React-Native supports component reuse by default. Components are created and reused. 
