Adaptive design is the practice of designing layouts that adapt to specific breakpoints and devices. Usually we consider the width of the device to determine where the layout should change, or adapt. Both Web and Android utilize responsive design concepts, like flexible grids and images, to create layouts that better respond to their context.

| Breakpoint | Cols | Gaps | Margins |
| :--------: | :--: | :--: | :-----: |
| Small 360  |  4   |  12  |   16    |
| Medium 600 |  8   |  24  |   32    |
| Large 1280 |  12  |  32  |   40    |

**Key Takeaways**

- Responsive Column Grid is made from columns, gutters, and margins
- Your Grid adapts to breakpoints, which can be customized to fit your layout
- A column grid keeps content organized and flexible
- Layouts can be broken into App Bar, Body, and Navigation

Keep in mind, larger screens can have increased visual noise as a result of more visible content. Sticking to a max line length of 60 characters will assist readability.

Similar items can be grouped together with white space or visible division to help guide the user through content. Implicit containment uses white space to visually group content to create container boundaries while explicit containment uses objects like divider lines and cards to group content together.

**Key Takeaways**

- Composition can scale at breakpoints.
- Grouping similar elements will help create more scannable content.
- Containment uses grouping to create visual boundaries that can be implicit or explicit.

Responsive patterns are common methods that help components adapt to their space.

Reposition is one of those patterns, where elements reflow on the screen to take advantage of the additional screen space.

Reflowing cards from a vertical orientation, moving a FAB to the nav rail, or dividing tabbed content into one space are all examples of Repositioning.

_Component Switching_
Components can adapt by switching out for functionality equivalent components that are better suited for large screens.

Navigation components that work on mobile can create ergonomic issues on large formats.

**Key Takeaways**

- Components and elements can change visibility at larger breakpoints.
- Components can adapt their width by remaining fixed or fluid.
- Components can adapt by switching out for functionality equivalent components at different breakpoints.
