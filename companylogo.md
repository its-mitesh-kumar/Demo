The Global Header in Red Hat Developer Hub now supports configurable **theme-specific company logos**. This enhancement allows platform teams to:

- Provide a single logo for both light and dark themes.

- Customize logos independently for light and dark themes.

- Control logo dimensions (width and height).

- Maintain backward compatibility with older configuration styles.

```
#...rest of the global Header configuration
red-hat-developer-hub.backstage-plugin-global-header:
      mountPoints:
        - mountPoint: application/header
          importName: GlobalHeader
          config:
            #position: above-sidebar 
            position: above-main-content #above-sidebar | above-main-content  
         - mountPoint: global.header/component
           importName: CompanyLogo
           config:
             priority: 200
             props:
               to: '/catalog'
               width: 300 #fallback to app.branding.fullLogoWidth,default is 150
               height: 200 #default is 40
               logo: 'data:image/png;base64,
               logo:
                 dark: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAATQAAACkCAMAAAAuT
                 light: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAgUAAABhCAMAAAB
```
In addition to the Global Header, We've enhanced the branding capabilities to support theme-specific logos in the sidebar as well.
- Single Logo for All Themes
```
app:
  branding:
    fullLogoWidth: 220  # Optional; defaults to 150px
    fullLogo: "data:image/svg+xml;base64,PHN2ZyB4bWxu…"
```
- Theme-Specific Logos
```
app:
  branding:
    fullLogoWidth: 220  # Optional
    fullLogo:
      light: "data:image/svg+xml;base64,PHN2ZyB4bWxu…"  # Shown in Light Theme
      dark:  "data:image/svg+xml;base64,PHN2ZyB4bWxu…"  # Shown in Dark Theme

```
