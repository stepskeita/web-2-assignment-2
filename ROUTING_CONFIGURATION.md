# Angular Router Configuration

## Routes Configuration

The Angular Router has been successfully configured in `src/app/app.routes.ts` with the following route mappings:

### Route Mappings:

| Route        | Component   | Description                        |
| ------------ | ----------- | ---------------------------------- |
| `/dashboard` | `Dashboard` | Main dashboard page with analytics |
| `/users`     | `Users`     | User management page               |
| `/products`  | `Products`  | Product management page            |
| `/reports`   | `Reports`   | Reports and analytics page         |
| `/settings`  | `Settings`  | Application settings page          |

### Default Route:

- **Empty path (`''`)** → Redirects to `/dashboard`
- **Wildcard (`**`)** → Redirects to `/dashboard` (404 fallback)

## Route Structure:

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
  { path: '**', redirectTo: '/dashboard' },
];
```

## Features:

✅ **Nested Routing**: All page routes are children of the `DashboardLayout` component  
✅ **Default Redirect**: Empty path redirects to `/dashboard`  
✅ **404 Handling**: Any invalid routes redirect to `/dashboard`  
✅ **Layout Integration**: Header and Sidebar are persistent across all pages  
✅ **Navigation**: Sidebar navigation with active link highlighting

## Testing Routes:

You can test the routes by visiting:

- http://localhost:4200/ (redirects to dashboard)
- http://localhost:4200/dashboard
- http://localhost:4200/users
- http://localhost:4200/products
- http://localhost:4200/reports
- http://localhost:4200/settings

All routes are fully functional with the sidebar navigation providing links to each page.
