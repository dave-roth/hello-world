# Tech Design for Alert
## Summary:
The Terra Alert component is a method for displaying information to the user regarding a current system condition, a clinical event, a future condition, advice, or general information.  Alerts provide contextual feedback messages for user actions.

The Terra Alert provides two levels of notification:
- Site-level alerts: Site-level alerts are intended to be displayed at the top of the viewport to convey page or system messages.  These alerts have the following characteristics:
  - Displays centered and fixed at the top of the browser window, overlaying any content underneath.
  - Have a max-width of 800px.
  - Always dismissible: the consuming application can indicate whether the alert is to be automatically dismissed in addition to being manually dismissible.
- Section-level alerts: Section-level alerts are intended to be displayed in context with the content they relate to. These alerts have the following characteristics:
  - Occupy 100% of the containing element's width.
  - Optionally dismissible.
  
The Terra Alert consists of the following visual components:
- Status Bar: a 2px wide bar displayed on the left (right when using dir=rtl) border of the component.  The color of the bar corresponds to the notification type configured by the application.
- Container: The background color of the container corresponds to the notification type configured by the application.  Its contents are as follows:
  - Icon: an icon displayed on the left (right when using dir=rtl) of the component.  The icon that is displayed corresponds to the notification type configured by the application.
  - Message Area: text displayed on the right (left when using dir=rtl) of the component.  The message area consists of the following:
    - Message Title: text that briefly summarizes the alert message.  This text is rendered in a bold font weight. The color of the text depends on the notification type configured by the application.
    - Message Text: text providing more detail of the alert.
  
The Terra Alert supports eight notification types:
- Alert: indicates that something requires the user's immediate attention.  Alerts of this type have the following characteristics:
  - Red status bar
  - Alert Icon
  - Red Message Title
  - Red Container background color
- Error: indicates that something has gone wrong.  Alerts of this type have the following characteristics:
  - Red status bar
  - Error icon
  - Red Message Title
  - Red Container background color
- Warning: indicates that some condition needs attention. Alerts of this type have the following characteristics:
  - Yellow status bar
  - Warning icon
  - Black message title
  - Yellow Container background color
- Required: indicates that something is required. Alerts of this type have the following characteristics:
  - Red status bar
  - Required icon
  - Black message title
  - Grey Container background color
- Advisory: indicates when a special situation arises. Alerts of this type have the following characteristics:
  - Purple status bar
  - Advisory icon
  - Black message title
  - Grey Container background color
- Custom: based on custom requirements of consuming application. Alerts of this type have the following characteristics:
  - Variable status bar color based on requirements of consuming application.
  - Variable icon based on requirements of consuming application
  - Black message title
  - Grey Container background color
- Information: provides neutral supplemental information. Alerts of this type have the following characteristics:
  - Blue status bar
  - Information icon
  - Black message title
  - Grey Container background color
- Confirmation: indicates when a user's action was successful. Alerts of this type have the following characteristics:
  - Green status bar
  - Confirmation icon
  - Black message title
  - Grey Container background color

## Requirements:
- [Alert Component Requirements](https://wiki.ucern.com/display/Orion/ORI040+Alert+Component)
- [Existing Alert in Legacy Terra](https://pages.github.cerner.com/orion/terra/site/indicators/alerts.html)
- [UI Approved Pattern](https://wiki.ucern.com/display/UserExperience/Terra-UI.terra-core%3AComponent%3AAlert)

## Requirements Added:
None.

## Requirements Dropped:
- The legacy Terra Alert supported a JavaScript API for showing an alert. There is no need to provide this support for the React component.

## Responsiveness:
The only responsive design requirement for this component is related to its width.
- For a Site-level Alert, the width of the component will fill the width of the containing element up to a maximum of 800px.
- For a Section-level Alert, the width of the component will always fill the width of the containing element. 

## Bidirectionality
The position of the elements are reversed when rendered using dir=rtl as compared to when it is rendered using dir=ltr.

## Accessibility
No specific accessibility requirements.

## React Props:
| Prop     | Type | Default | Description  |
|----------|------|---------|--------------|
| level | string | null    | JSX children |

## Example:
```
<Component
  intent="primary"
  size="huge"
/>
```

## CSS Classes:
| Selector         | Description |
|------------------|-------------|
| .terra-Component | ....        |
