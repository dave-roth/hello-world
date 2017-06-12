# Tech Design for Alert
## Summary:
The Terra Alert component is a method for displaying information to the user regarding a current system condition, a clinical event, a future condition, advice, or general information.  Alerts provide contextual feedback messages for user actions.
  
The Terra Alert consists of the following visual components:
- Status Bar: a 2px wide bar displayed on the left (right when using dir=rtl) border of the component.  The color of the bar corresponds to the notification type configured by the application.
- Container: The background color of the container corresponds to the notification type configured by the application.  The Terra Arrange component can be used for positioning/centering the contents of the container and for handling bidirectionality.  Its contents are as follows:
  - Icon: an icon corresponding to the notification type of the alert.  The Terra Icon component will be used to provide the appropriate icon for the alert type. The Icon will be rendered in the fitStart container of Terra Arrange component.
  - Message Area: The Message Area will be rendered in the fill container of the Terra Arrange component.  The message area consists of the following:
    - Title: text that briefly summarizes the alert message.  This text is rendered in a bold font weight. The color of the text depends on the notification type configured by the application.
    - Message: text or HTML content providing more detail of the alert.
  - Action Area: Optional area of the Alert containing actionable elements. The Action Area will be rendered in the fitEnd container of the Terra Arrange component.  This area can include one or both of the following:
    - Custom Action Element: The consuming application can include an alert-specific action element which would allow the user to act on the alert. This would typically be a button, but can consist of other HTML elements if desired.
    - Dismiss button: The consuming application can configure whether the Alert is dismissible or not based on whether the onDismiss prop is provided. If it is dismissible, a Dismiss button will be included in the Action Area.  It will be rendered at the end of the Action Area.
  
The Terra Alert supports eight notification types:
- Alert: indicates that something requires the user's immediate attention.  Alerts of this type have the following characteristics:
  - Red status bar ($terra-red-70)
  - Alert Icon: use <IconAlert/> component.
  - Red Message Title ($terra-red-70)
  - Red Container background color ($terra-red-20)
- Error: indicates that something has gone wrong.  Alerts of this type have the following characteristics:
  - Red status bar ($terra-red-70)
  - Error icon: use <IconError/> component.
  - Red Message Title ($terra-red-70)
  - Red Container background color ($terra-red-20)
- Warning: indicates that some condition needs attention. Alerts of this type have the following characteristics:
  - Yellow status bar ($terra-yellow-60)
  - Warning icon: use <IconWarning/> component.
  - Black message title 
  - Yellow Container background color ($terra-yellow-20)
- Required: indicates that something is required. Alerts of this type have the following characteristics:
  - Red status bar ($terra-red-70)
  - Required icon: use <IconRequired/> component.
  - Black message title
  - Grey Container background color ($terra-grey-5)
- Advisory: indicates when a special situation arises. Alerts of this type have the following characteristics:
  - Purple status bar ($terra-purple-80)
  - Advisory icon: use <IconDiamond/> component.
  - Black message title
  - Grey Container background color ($terra-grey-5)
- Information: provides neutral supplemental information. Alerts of this type have the following characteristics:
  - Blue status bar ($terra-blue-70)
  - Information icon: use <IconInformation/> component.
  - Black message title
  - Grey Container background color ($terra-grey-5)
- Confirmation: indicates when a user's action was successful. Alerts of this type have the following characteristics:
  - Green status bar ($terra-green-60)
  - Confirmation icon: use <IconSuccess/> component.
  - Black message title
  - Grey Container background color ($terra-grey-5)
- Custom: based on custom requirements of consuming application. Alerts of this type have the following characteristics:
  - Variable status bar color based on requirements of consuming application.
  - Variable icon based on requirements of consuming application. Application will provide an element of either a Terra Icon or Terra Image for the icon if desired.
  - Black message title
  - Grey Container background color ($terra-grey-5)

## Requirements:
- [Alert Component Requirements](https://wiki.ucern.com/display/Orion/ORI040+Alert+Component)
- [Existing Alert in Legacy Terra](https://pages.github.cerner.com/orion/terra/site/indicators/alerts.html)
- [UI Approved Pattern](https://wiki.ucern.com/display/UserExperience/Terra-UI.terra-core%3AComponent%3AAlert)

## Requirements Added:
None.

## Requirements Dropped:
- The legacy Terra Alert supported a JavaScript API for showing an alert. There is no need to provide this support for the React component.
- Legacy Terra supported site-level and section-level Alerts.  The multiple levels of Alerts is listed as "TBD" in the requirements document so they are not included in this initial design.

## Responsiveness:
 The Action Area of the alert will render to the right (left if using dir=rtl) of the Message Area.  However, if the screen size is below the "tiny" breakpoint, the Action Area would be rendered below the Message Area. 

## Bidirectionality
As described above, the Terra Arrange component will be used to position the different areas of the Terra Alert component appropriately based on whether dir=ltr or dir=rtl is being used.  In addition, the status bar will also need to be positioned based on the direction being used.

## Accessibility
No specific accessibility requirements.

## React Props:
| Prop                  | Type    | Default | Description  |
|-----------------------|---------|---------|--------------|
| type                  | string  | ""      | (Required prop) The notification level for the alert. Allowable values are "alert", "error", "warning", "required", "advisory", "custom", "information" and "confirmation".  These values will be available as constants in an attribute of the Alert component.  See below for how the constants will be defined.  |
| title                 | string  | ""      | Optional title of the message to be displayed in the Alert. For the pre-defined alert types, if no title is provided, then a default internationalized title appropriate for the type will be used. For the custom alert type, no default title can be applied so it is the responsibility of the consuming application to supply the title for a custom alert. |
| children              | string or element  | null      | The message content for the alert. The content can simply be a text string or it can be an HTML element if the consuming application requires formatted content.  |
| onDismiss             | func    | null    | Callback function to be called when the Dismiss button is clicked.  The Dismiss button will only be rendered when this prop is provided by the application.  |
| alertAction           | element | null    | An HTML element, typically a button, that will be added to the Action Area of the alert.  This action element is controlled by the consuming application.  The Terra Alert component itself will not take any action when the user interacts with this element.  |
| customStatusColor     | string  | ""      | The color to be used for the status bar for a Custom Alert type.  |
| customIcon            | element | null    | The icon to be used for the Custom Alert type.  This can be the output of a Terra Icon or Terra Image component. |

The Alert component will provide an attribute (Alert.Types) containing constants that can be used when specifying the alert type.
```
const AlertTypes = {
  ALERT: "alert",
  ERROR: "error",
  WARNING: "warning",
  REQUIRED: "required",
  ADVISORY: "advisory",
  CUSTOM: "custom",
  INFORMATION: "information",
  CONFIRMATION: "confirmation"
}
. . .
Alert.Types = AlertTypes;
```

## Example:
The following example shows how you would create an Alert of type error using the default title.
```
<Alert type=Alert.Types.ERROR>This is the error text.</Alert>

```

The following example shows how you would create an Alert of type custom that uses the <IconHelp/> Terra Icon component and sets the status bar color to orange.
```
<Alert
  type=Alert.Types.CUSTOM
  title="Help!"
  CustomAlertStatusColor="orange"
  CustomAlertIcon={<IconHelp/>}
/>
  This is the custom text.
</Alert>
```

The following example shows how you would create an advisory Alert, overriding the default title, providing some formatted HTML for the message, allowing it to be dismissible and providing an action button.
```
<Alert
  type=Alert.Types.ADVISORY
  title="Advisory Notice!"
  onDismiss={this.handleDismiss},
  alertAction={<BUTTON ...>Custom Action</BUTTON>}
>
  <SPAN>This is an <U>advisory</U> notice.</SPAN>
</Alert>
```
  


## CSS Classes:
| Selector                   | Description |
|----------------------------|-------------|
| .terra-Alert               | class for Alert container            |
| .terra-Alert--alert        | class for Alert of type alert        |
| .terra-Alert--error        | class for Alert of type error        |
| .terra-Alert--warning      | class for Alert of type warning      |
| .terra-Alert--required     | class for Alert of type required     |
| .terra-Alert--advisory     | class for Alert of type advisory     |
| .terra-Alert--custom       | class for Alert of type custom       |
| .terra-Alert--information  | class for Alert of type information  |
| .terra-Alert--confirmation | class for Alert of type confirmation |
| .terra-Alert--title        | class for Alert title                |
