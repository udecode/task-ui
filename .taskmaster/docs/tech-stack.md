# Taskmaster Circle - Tech Stack Documentation

## Overview

Taskmaster Circle is a modern web application built with Next.js 15 and React 19, designed as a visual interface for the Taskmaster CLI tool. The application uses a component-driven architecture with TypeScript for type safety and Tailwind CSS v4 for styling. Currently implemented as a frontend-only application with mock data, ready for integration with Taskmaster's file-based task management system.

- **Architecture**: Frontend-only SPA with planned local file system integration
- **Stack Type**: Modern React with Next.js App Router
- **Development Stage**: Pre-MVP UI template

## Programming Language & Runtime

### TypeScript

- **Version**: 5.x with strict mode enabled
- **Target**: ES2017
- **Module Resolution**: Bundler
- **Path Aliases**: Configured with `@/*` for clean imports
- **Type Checking**: Strict mode with all checks enabled

### JavaScript Runtime

- **Node.js**: Required for development and build processes
- **Package Manager**: pnpm (recommended based on lockfile)
- **ECMAScript**: Modern ES2017+ features

## Frontend

### Core Framework

- **Next.js 15.2.4**

   - App Router architecture
   - TurboPack enabled for faster development builds
   - Server Components support
   - Built-in optimizations

- **React 19.0.0**
   - Latest React version
   - Server Components compatible
   - Concurrent features enabled

### UI Components & Libraries

#### Component System

- **shadcn/ui**: Component library built on Radix UI
- **Radix UI Primitives**:
   - Alert Dialog, Avatar, Checkbox, Collapsible
   - Context Menu, Dialog, Dropdown Menu
   - Label, Menubar, Navigation Menu
   - Popover, Progress, Radio Group
   - Select, Separator, Slider, Switch
   - Tabs, Toast, Toggle, Toggle Group, Tooltip

#### Styling

- **Tailwind CSS v4.0.0-beta.14**

   - Latest v4 beta with improved performance
   - Utility-first CSS framework
   - PostCSS integration
   - Custom configuration with animations

- **CSS Utilities**:
   - `clsx`: Conditional class names
   - `tailwind-merge`: Merge Tailwind classes correctly
   - `class-variance-authority`: Component variants
   - `tailwindcss-animate`: Animation utilities

### State Management

- **Zustand 5.0.3**
   - Lightweight state management
   - TypeScript support
   - Multiple stores for different features:
      - Filters store
      - Issues store
      - Members store
      - Projects store
      - Teams store

### Forms & Validation

- **React Hook Form 7.54.2**: Form state management
- **Zod 3.24.2**: Schema validation
- **@hookform/resolvers 3.9.1**: Integration between RHF and Zod

### Additional UI Libraries

- **Motion 12.4.10**: Animation library
- **react-dnd 16.0.1**: Drag and drop functionality
- **cmdk 1.0.0**: Command menu (Cmd+K) component
- **sonner 2.0.1**: Toast notifications
- **recharts 2.15.1**: Data visualization charts
- **react-day-picker 8.10.1**: Date picker component
- **next-themes 0.4.4**: Theme management (dark/light mode)

### Icons

- **lucide-react 476.0**: Primary icon library
- **@remixicon/react 4.6.0**: Additional icons

### Utilities

- **date-fns 4.1.0**: Date manipulation
- **uuid 11.1.0**: Unique ID generation
- **@kayron013/lexorank 2.0.0**: Lexicographic ranking for ordering
- **usehooks-ts 3.1.1**: TypeScript React hooks collection

## Backend

Currently not implemented. The application uses mock data and is prepared for future integration with:

- Local file system access for `.taskmaster` files
- File watching for real-time updates
- CLI command execution for write operations

## Database & Storage

### Current State

- **Mock Data**: Static TypeScript files in `/mock-data/`
- **No Database**: Frontend-only implementation
- **Local Storage**: Browser storage for user preferences

### Planned Integration

- **File System**: Direct access to `.taskmaster/tasks/tasks.json`
- **Watch Mode**: File system watching for real-time updates
- **No Traditional Database**: Taskmaster uses file-based storage

## Development Tools & Workflow

### Build Tools

- **Next.js Built-in Build System**
   - TurboPack for development
   - Webpack 5 for production builds
- **PostCSS**: CSS processing for Tailwind

### Code Quality

- **ESLint 9**

   - Next.js recommended configuration
   - TypeScript rules
   - React rules

- **Prettier 3.5.2**
   - Code formatting
   - Custom configuration:
      - Tab width: 3 spaces
      - Single quotes
      - No trailing commas
      - No semicolons

### Git Hooks

- **Husky 9.1.7**: Git hooks management
- **lint-staged 15.4.3**: Run linters on staged files
   - Prettier formatting on commit
   - ESLint checks

### Development Scripts

```json
{
   "dev": "next dev --turbopack",
   "build": "next build",
   "start": "next start",
   "lint": "next lint",
   "format": "prettier --write ."
}
```

## Deployment & Infrastructure

### Current Status

- **Local Development Only**: No deployment configuration
- **Development Server**: Next.js dev server with TurboPack

### Future Considerations

- Local-first application (like Prisma Studio)
- Potential desktop app packaging (Electron/Tauri)
- No cloud deployment needed for core functionality

## External Integrations

### Current

- **None**: Standalone frontend application

### Planned

- **Taskmaster CLI**: File system integration
- **File System APIs**: For reading/watching `.taskmaster` files
- **Operating System**: File system events for real-time updates

## Quality Assurance & Testing

### Current State

- **No Test Framework**: Focus on implementation for Pre-MVP
- **Manual Testing**: Developer testing during development
- **Type Safety**: TypeScript provides compile-time checks

### Code Quality Tools

- ESLint for code standards
- Prettier for formatting consistency
- TypeScript for type safety
- Git hooks for pre-commit checks

## Project Structure

### Directory Organization

```
/
   app/                    # Next.js App Router pages
      [orgId]/           # Dynamic organization routes
          issues/        # Issues management
          projects/      # Projects view
          teams/         # Teams management
   components/
      ui/               # Reusable UI components (shadcn/ui)
      common/           # Feature-specific components
         issues/       # Issue-related components
         members/      # Member components
         projects/     # Project components
         teams/        # Team components
      layout/           # Layout components
          header/       # App headers
          sidebar/      # Navigation sidebar
   lib/                   # Utilities and helpers
   mock-data/            # Development mock data
   public/               # Static assets
   store/                # Zustand state stores
   styles/               # Global styles and Tailwind
```

### Configuration Files

- `tsconfig.json`: TypeScript configuration
- `next.config.ts`: Next.js configuration
- `tailwind.config.ts`: Tailwind CSS configuration
- `postcss.config.mjs`: PostCSS configuration
- `.eslintrc.json`: ESLint rules
- `.prettierrc`: Prettier formatting rules

### Module System

- ES Modules throughout
- Path aliases with `@/` prefix
- Component exports follow consistent patterns

## Schemas & Data Models

### Current Mock Data Models

#### Issue

```typescript
interface Issue {
   id: string;
   identifier: string; // e.g., "LNUI-101"
   title: string;
   description: string;
   status: Status; // backlog | todo | in_progress | done | cancelled
   priority: Priority; // urgent | high | medium | low | no_priority
   assignee: User | null;
   labels: Label[];
   createdAt: string;
   cycleId: string;
   project?: Project;
   subissues?: string[];
   rank: string; // LexoRank for ordering
   dueDate?: string;
}
```

#### Project

```typescript
interface Project {
   id: string;
   name: string;
   color: string;
   health: 'on-track' | 'at-risk' | 'off-track';
   teamIds: string[];
   leadId: string;
   memberIds: string[];
   targetDate: string;
   createdAt: string;
}
```

#### Team

```typescript
interface Team {
   id: string;
   name: string;
   organizationId: string;
   memberIds: string[];
   projectIds: string[];
   cycleIds: string[];
   createdAt: string;
}
```

### Planned Taskmaster Integration

The mock data structure aligns well with Taskmaster's data model:

- Issues � Tasks
- Projects � Tag contexts
- Status mapping matches Taskmaster statuses
- Priority levels compatible
- Subtask hierarchy supported

### Type Definitions

- Comprehensive TypeScript interfaces
- Zod schemas for runtime validation
- Consistent data model across components
- Ready for Taskmaster data transformation
