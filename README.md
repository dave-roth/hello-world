# Tech Design for Alert
## Summary:
The Terra Alert component is a method for displaying information to the user regarding a current system condition, a clinical event, a future condition, advice, or general information.  Alerts provide contextual feedback messages for user actions.
  
The Terra Alert consists of the following visual components:
- Status Bar: a 2px wide bar displayed on the left (right when using dir=rtl) border of the component.  The color of the bar corresponds to the notification type configured by the application.
- Container: The background color of the container corresponds to the notification type configured by the application.  The Terra Arrange component can be used for positioning/centering the contents of the container and for handling bidirectionality.  Its contents are as follows:
  - Icon: an icon displayed on the left (right when using dir=rtl) of the container.  The icon that is displayed corresponds to the notification type configured by the application.  The Terra Icon component will be used to provide the appropriate icon for the alert type.
  - Message Area: text displayed on the right (left when using dir=rtl) of the component.  The message area consists of the following:
    - Message Title: text that briefly summarizes the alert message.  This text is rendered in a bold font weight. The color of the text depends on the notification type configured by the application.
    - Message Text: text providing more detail of the alert.
  
The Terra Alert supports eight notification types:
- Alert: indicates that something requires the user's immediate attention.  Alerts of this type have the following characteristics:
  - Red status bar
  - Alert Icon: use <IconAlert/> component.
  - Red Message Title
  - Red Container background color
- Error: indicates that something has gone wrong.  Alerts of this type have the following characteristics:
  - Red status bar
  - Error icon: use <IconError/> component.
  - Red Message Title
  - Red Container background color
- Warning: indicates that some condition needs attention. Alerts of this type have the following characteristics:
  - Yellow status bar
  - Warning icon: use <IconWarning/> component.
  - Black message title
  - Yellow Container background color
- Required: indicates that something is required. Alerts of this type have the following characteristics:
  - Red status bar
  - Required icon: use <IconRequired/> component.
  - Black message title
  - Grey Container background color
- Advisory: indicates when a special situation arises. Alerts of this type have the following characteristics:
  - Purple status bar
  - Advisory icon: use <IconDiamond/> component.
  - Black message title
  - Grey Container background color
- Custom: based on custom requirements of consuming application. Alerts of this type have the following characteristics:
  - Variable status bar color based on requirements of consuming application.
  - Variable icon based on requirements of consuming application. Application will provide an element of either a Terra Icon or Terra Image for the icon if desired.
  - Black message title
  - Grey Container background color
- Information: provides neutral supplemental information. Alerts of this type have the following characteristics:
  - Blue status bar
  - Information icon: use <IconInformation/> component.
  - Black message title
  - Grey Container background color
- Confirmation: indicates when a user's action was successful. Alerts of this type have the following characteristics:
  - Green status bar
  - Confirmation icon: use <IconSuccess/> component.
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
- Legacy Terra supported site-level and section-level Alerts.  The multiple levels of Alerts is listed as "TBD" in the requirements document so they are not included in this initial design.
- Legacy Terra supported dismissible Alerts. Dismissible Alerts is listed as "TBD" in the requirements document so they are not included in this initial design.

## Responsiveness:
The only responsive design requirement for this component is related to its width. The width of the component will always fill the width of the containing element. 

## Bidirectionality
The position of the elements are reversed when rendered using dir=rtl as compared to when it is rendered using dir=ltr.

## Accessibility
No specific accessibility requirements.

## React Props:
| Prop                  | Type    | Default | Description  |
|-----------------------|---------|---------|--------------|
| type                  | string  | ""      | (Required prop) The notification level for the alert. Allowable values are "alert", "error", "warning", "required", "advisory", "custom", "information" and "confirmation".  These values will be available as exported constants.  See below for how the constants will be defined.  |
| title                 | string  | ""      | (Required prop) Title of the message to be displayed in the Alert.  |
| text                  | string  | ""      | (Required prop) Text of the message to be displayed in the Alert.  |
| customAlertStatusColor| string  | ""      | The color to be used for the status bar for a Custom Alert type.  |
| customAlertIcon       | element | null    | The icon to be used for the Custom Alert type.  This can be the output of a Terra Icon or Terra Image component. |

The Alert component will export constants that can be used when specifying the alert type.
```
const Terra_Alert_Types = {
  ALERT: "alert",
  ERROR: "error",
  WARNING: "warning",
  REQUIRED: "required",
  ADVISORY: "advisory",
  CUSTOM: "custom",
  INFORMATION: "information",
  CONFIRMATION: "confirmation"
}
```

## Example:
The following example shows how you would create an Alert of type error.
```
<Alert
  type=Terra_Alert_Types.ERROR
  messageTitle="Error!"
  messageText="An error has occurred."
/>
```

The following example shows how you would create an Alert of type custom that uses the <IconHelp/> Terra Icon component.
```
<Alert
  type=Terra_Alert_Types.CUSTOM
  messageTitle="Help!"
  messageText="Follow these instructions to complete your task."
  CustomAlertStatusColor="orange"
  CustomAlertIcon={<IconHelp/>}
/>
```


## CSS Classes:
| Selector                  | Description |
|---------------------------|-------------|
| .terra-Alert              | class for Alert container            |
| .terra-Alert--alert        | class for Alert of type alert        |
| .terra-Alert--error        | class for Alert of type error        |
| .terra-Alert--warning      | class for Alert of type warning      |
| .terra-Alert--required     | class for Alert of type required     |
| .terra-Alert--advisory     | class for Alert of type advisory     |
| .terra-Alert--custom       | class for Alert of type custom       |
| .terra-Alert--information  | class for Alert of type information  |
| .terra-Alert--confirmation | class for Alert of type confirmation |
| .terra-Alert--title        | class for Alert title                |
