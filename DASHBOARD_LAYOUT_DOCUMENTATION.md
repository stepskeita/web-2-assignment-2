# DashboardLayoutComponent Implementation

## Overview

The `DashboardLayoutComponent` provides the main layout structure for the admin dashboard application with a fixed header, sidebar navigation, and dynamic content area.

## Component Structure

### Files:

- `dashboard-layout.ts` - Component class and configuration
- `dashboard-layout.html` - Template structure
- `dashboard-layout.scss` - Styling and responsive design

## Layout Architecture

```
┌─────────────────────────────────────────┐
│              HEADER (Fixed)              │
│  ┌─────────────────────────────────────┐ │
│  │ [☰] Admin Dashboard    [User Avatar]│ │
│  └─────────────────────────────────────┘ │
├─────────────┬───────────────────────────┤
│   SIDEBAR   │       MAIN CONTENT        │
│   (Fixed)   │     (<router-outlet>)     │
│             │                           │
│ 📊Dashboard │  ┌─────────────────────┐  │
│ 👥Users     │  │                     │  │
│ 📦Products  │  │   Dynamic Content   │  │
│ 📈Reports   │  │   Area for Pages    │  │
│ ⚙️Settings   │  │                     │  │
│             │  └─────────────────────┘  │
└─────────────┴───────────────────────────┘
```

## Key Features

### ✅ **Fixed Header**

- **Position**: `position: fixed; top: 0;`
- **Height**: `60px`
- **Z-index**: `1000` (stays on top)
- **Content**: Logo/branding and user profile
- **Mobile**: Includes hamburger menu button

### ✅ **Fixed Sidebar**

- **Position**: `position: fixed; left: 0; top: 60px;`
- **Width**: `250px` (responsive: 200px on tablets)
- **Height**: `calc(100vh - 60px)`
- **Navigation**: Router links with active states
- **Mobile**: Hidden by default, toggleable

### ✅ **Dynamic Main Content**

- **Position**: Offset by sidebar and header margins
- **Margins**: `margin-top: 60px; margin-left: 250px;`
- **Content**: `<router-outlet>` for page components
- **Responsive**: Adjusts margins based on screen size

## Responsive Design

### Desktop (> 1024px)

```scss
.main-content {
  margin-left: 250px;
  width: calc(100% - 250px);
}
```

### Tablet (768px - 1024px)

```scss
.main-content {
  margin-left: 200px;
  width: calc(100% - 200px);
}
```

### Mobile (< 768px)

```scss
.main-content {
  margin-left: 0;
  width: 100%;
}
.sidebar {
  transform: translateX(-100%); // Hidden
}
```

## Component Implementation

### Template Structure

```html
<div class="dashboard-layout">
  <app-header></app-header>
  <app-sidebar></app-sidebar>
  <main class="main-content">
    <router-outlet></router-outlet>
  </main>
</div>
```

### Component Class

```typescript
@Component({
  selector: 'app-dashboard-layout',
  imports: [RouterOutlet, Header, Sidebar],
  templateUrl: './dashboard-layout.html',
  styleUrl: './dashboard-layout.scss',
})
export class DashboardLayout {}
```

## Router Integration

The layout is integrated with Angular Router as a parent route:

```typescript
export const routes: Routes = [
  {
    path: '',
    component: DashboardLayout,
    children: [
      { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
      { path: 'dashboard', component: Dashboard },
      { path: 'users', component: Users },
      { path: 'products', component: Products },
      { path: 'reports', component: Reports },
      { path: 'settings', component: Settings },
    ],
  },
];
```

## Benefits

- **🎯 Consistent Layout**: Header and sidebar persist across all pages
- **📱 Responsive Design**: Adapts to different screen sizes
- **🔄 Dynamic Content**: Pages render in main content area via router-outlet
- **⚡ Performance**: Fixed positioning for smooth scrolling
- **🎨 Professional UI**: Clean, modern admin dashboard appearance
- **♿ Accessibility**: Proper semantic HTML structure

## Usage

The DashboardLayoutComponent automatically wraps all child routes, providing a consistent layout structure for the entire admin dashboard application. Page components render within the main content area while maintaining the fixed header and sidebar navigation.
