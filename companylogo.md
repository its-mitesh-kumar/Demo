 Global Header: Theme-Specific Company Logo Support
=====================================================

The Global Header in **Red Hat Developer Hub (RHDH)** now supports configurable **theme-specific company logos** with full control over navigation, theming, sizing, and fallback behavior.

* * *

 Key Enhancements
------------------

*    Company logo is now **part of the Global Header by default**.
    
*    Support for a **single logo** used across both Light and Dark themes.
    
*    Support for **theme-specific logos** (separate logos for Light and Dark themes).
    
*    Ability to **control logo dimensions** via width and height props.
    
*    **Clickable logo**: custom navigation path can be configured.
    
*    **Backward compatibility** with older `app.branding.fullLogo` configurations.
    

* * *

⚙️ Configuration Example
------------------------

```
# ...rest of the global header configuration
red-hat-developer-hub.backstage-plugin-global-header:
  mountPoints:
    - mountPoint: application/header
      importName: GlobalHeader
      config:
        position: above-main-content  # Options: above-sidebar | above-main-content 

    - mountPoint: global.header/component
      importName: CompanyLogo
      config:
        priority: 200
        props:
          to: '/catalog'  # Path to navigate when logo is clicked
          width: 300       # Optional; fallback chain applies
          height: 200      # Optional; default max height is 40px
          #logo: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAATQAAACkCAMAAAAuT...' #Single logo for all theme.
          logo:
            dark: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAATQAAACkCAMAAAAuT...' #will be shown in dark theme
            light: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAgUAAABhCAMAAAB...'  #will be shown in light theme

```

* * *

 Fallback Behavior
--------------------

###  Logo Source Priority

1.  `CompanyLogo` props (`logo` / `logo.light` / `logo.dark`)
    
2.  `app.branding.fullLogo`
    
3.  Default RHDH theme-specific logo
    

* * *

 Logo Sizing Behavior
-----------------------

###  Width Resolution Priority

1.  `props.width` (from the dynamic plugin configuration)
    
2.  `app.branding.fullLogoWidth` (from `app-config.yaml`)
    
3.  Default: `150px`
    

###  Height Resolution Priority

1.  `props.height` (from configuration)
    
2.  Default maximum height: `40px` (applied automatically if not specified)
    

> **Note:** Increasing the `height` also increases the overall height of the Global Header.

###  Rendering Behavior

*   The logo uses `object-fit: contain` to **maintain original aspect ratio**.
    
*   The image is **never cropped or distorted**.
    
*   If the configured `width` would result in a height greater than the allowed maximum (default: 40px), it is **automatically scaled down**.
    
*   This means: in some cases, changing only the width may **not visibly affect** the logo unless height is also adjusted.
    

* * *

 Sidebar Support
------------------

In addition to the Global Header, **theme-specific logo support is also available in the sidebar**.

###  Single Logo for All Themes

```
app:
  branding:
    fullLogoWidth: 220
    fullLogo: "data:image/svg+xml;base64,PHN2ZyB4bWxu…"

```

###  Theme-Specific Logos

```
app:
  branding:
    fullLogoWidth: 220
    fullLogo:
      light: "data:image/svg+xml;base64,PHN2ZyB4bWxu…"  # Light Theme
      dark:  "data:image/svg+xml;base64,PHN2ZyB4bWxu…"  # Dark Theme

```


