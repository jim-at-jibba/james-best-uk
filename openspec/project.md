# Project Context

## Purpose
Personal portfolio website for James Best, a software engineer from Bristol, UK. The site showcases featured projects, blog articles, and professional information using a retro-inspired design theme.

## Tech Stack
- **Framework**: Astro 5.3.1 (static site generator)
- **Language**: TypeScript with strict type checking
- **Styling**: Tailwind CSS 4.0.8 with custom theme variables
- **Typography**: Tailwind CSS Typography plugin
- **Fonts**: Literata Variable (serif), Press Start 2P (display), IBM Plex Mono (monospace)
- **Build Tool**: Vite (built into Astro)
- **Package Manager**: pnpm (primary), with support for yarn and bun

## Project Conventions

### Code Style
- TypeScript strict mode enabled with `@ts-check`
- Astro component files use `.astro` extension
- Component naming: PascalCase for components (e.g., `Hero.astro`, `FeaturedProjects.astro`)
- File organization: Feature-based structure under `src/components/` and `src/pages/`
- CSS custom variables follow `--zag-*` naming convention for theme consistency
- Dark mode support using `:where(.dark, .dark *)` CSS selectors

### Architecture Patterns
- **Component-based architecture**: Reusable Astro components with slots for composition
- **Layout system**: Common layouts in `src/layouts/` (Layout.astro, BlogLayout.astro, ProjectLayout.astro)
- **Content management**: Markdown files for blog posts and project descriptions
- **Theme system**: CSS custom variables with dark/light mode support
- **Data organization**: Centralized configuration in `src/lib/variables.ts` and `src/lib/featured.ts`

### Testing Strategy
- No formal testing framework currently implemented
- Manual testing through Astro dev server and build validation
- Lighthouse performance optimization (targets 100/100 score)
- Accessibility testing built into theme development

### Git Workflow
- Conventional commits with clear, descriptive messages
- Feature branches for new development
- Main branch for deployed production code
- No automated CI/CD pipeline currently configured

## Domain Context
This is a personal portfolio website targeting:
- **Primary audience**: Potential employers, clients, and tech community
- **Content focus**: Software engineering projects, technical blog posts, professional experience
- **Design aesthetic**: Retro-inspired with modern performance and accessibility
- **Geographic context**: Bristol, UK based developer
- **Professional context**: Lean Engineer at Breedr

## Important Constraints
- **Performance**: Must maintain 100/100 Lighthouse score
- **Accessibility**: Fully accessible with proper ARIA labels and semantic HTML
- **Responsive design**: Must work across all device sizes
- **SEO optimization**: Proper meta tags, structured data, and canonical URLs
- **Dark mode**: Full dark/light theme support with system preference detection
- **Static generation**: No server-side rendering or dynamic content

## External Dependencies
- **CDN fonts**: Fontsource for Literata Variable, Press Start 2P, and IBM Plex Mono
- **Social platforms**: GitHub and Twitter profile integration
- **Image hosting**: Profile and project images hosted locally in `/public/`
- **Theme inspiration**: Based on Zaggonaut theme template
