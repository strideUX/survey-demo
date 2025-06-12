# Survey Color Palette Implementation Guide

## Available Color Variables

The following CSS custom properties are now available in `:root` for easy theming:

### Primary Colors
- `--survey-primary`: Main brand color for buttons, progress bar, active selections
- `--survey-primary-hover`: Hover state for primary elements

### Secondary Colors  
- `--survey-secondary`: Accent color for secondary elements
- `--survey-secondary-hover`: Hover state for secondary elements

### Background Colors
- `--survey-background`: Main page background
- `--survey-card-background`: Card/container background

### Text Colors
- `--survey-text-primary`: Headings, primary text
- `--survey-text-secondary`: Secondary text, labels  
- `--survey-text-muted`: Muted text, placeholders

### Error Colors
- `--survey-error`: Error messages and validation
- `--survey-error-bg`: Error background color

### Border Colors
- `--survey-border`: Default borders
- `--survey-border-focus`: Focused input borders

## Implementation Examples

### In Tailwind Classes (using arbitrary values):
```html
<!-- Primary button -->
<button class="px-6 py-2 rounded-md text-white transition" 
        style="background-color: var(--survey-primary);">
  Next →
</button>

<!-- Card background -->
<div class="rounded-xl shadow-lg p-8" 
     style="background-color: var(--survey-card-background);">
  Card content
</div>

<!-- Text colors -->
<h2 style="color: var(--survey-text-primary);">Main Heading</h2>
<p style="color: var(--survey-text-secondary);">Secondary text</p>
```

### In Style Attributes:
```html
<!-- Progress bar -->
<div class="w-full h-1" style="background-color: var(--survey-border);">
  <div class="h-full" style="background-color: var(--survey-primary); width: 66.67%;"></div>
</div>

<!-- Input with focus state -->
<input class="border rounded-md px-4 py-2" 
       style="border-color: var(--survey-border); 
              background-color: var(--survey-card-background);"
       onfocus="this.style.borderColor = 'var(--survey-border-focus)'" />
```

### Changing Themes

To create different themes, simply update the CSS variables in `src/app.css`:

```css
/* Blue Theme (Current) */
:root {
  --survey-primary: #1976d2;
  --survey-background: #F7F7F5;
}

/* Green Theme Example */
:root {
  --survey-primary: #2e7d32;
  --survey-background: #f1f8e9;
}

/* Purple Theme Example */
:root {
  --survey-primary: #7b1fa2;
  --survey-background: #f3e5f5;
}
```

## Next Steps

1. **Replace hardcoded colors**: Replace current style attributes and Tailwind colors with CSS variables
2. **Test themes**: Create different theme configurations by updating the CSS variables
3. **Add hover states**: Use the hover variants for interactive elements
4. **Validate consistency**: Ensure all UI elements use the same color system 