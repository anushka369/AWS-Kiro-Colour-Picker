# Implementation Plan

- [x] 1. Set up project structure and development environment
  - Initialize Vite + React + TypeScript project
  - Configure TypeScript with strict mode
  - Install dependencies: styled-components, fast-check, vitest, @testing-library/react
  - Set up basic project structure with src/components, src/utils, src/hooks folders
  - Create index.html and basic App.tsx entry point
  - _Requirements: All_

- [x] 2. Implement core color utilities and conversions
  - [x] 2.1 Create color type definitions and interfaces
    - Define Color, RGB, HSL, Palette interfaces in types.ts
    - _Requirements: 1.1, 3.3, 3.4_
  
  - [x] 2.2 Implement color conversion functions
    - Write hexToRgb, rgbToHex, rgbToHsl, hslToRgb, hexToHsl, hslToHex functions
    - Add input validation and clamping for out-of-range values
    - _Requirements: 3.3, 3.4_
  
  - [x] 2.3 Write property test for color conversion round-trips
    - **Property 13 (adapted): Color conversion round-trips**
    - **Validates: Requirements 3.3, 3.4**
  
  - [x] 2.4 Write unit tests for color conversions
    - Test known conversion examples (e.g., #FF0000 = rgb(255,0,0) = hsl(0,100%,50%))
    - Test edge cases (black, white, grays)
    - _Requirements: 3.3, 3.4_

- [x] 3. Implement color harmony algorithms
  - [x] 3.1 Create harmony rule generators
    - Implement generateAnalogousPalette (±30° hue variations)
    - Implement generateComplementaryPalette (180° hue offset)
    - Implement generateTriadicPalette (120° hue spacing)
    - Implement generateTetradicPalette (90° hue spacing)
    - Implement generateMonochromaticPalette (same hue, varied saturation/lightness)
    - _Requirements: 1.3_
  
  - [x] 3.2 Implement palette generation with lock support
    - Create generateRandomPalette function that respects locked colors
    - Randomly select harmony rule for generation
    - Ensure exactly 5 colors in every palette
    - _Requirements: 1.2, 2.2, 2.3_
  
  - [x] 3.3 Write property test for palette generation validity
    - **Property 1: Palette generation produces valid palettes**
    - **Validates: Requirements 1.2**
  
  - [x] 3.4 Write property test for harmony rule conformance
    - **Property 2: Generated palettes follow harmony rules**
    - **Validates: Requirements 1.3**
  
  - [x] 3.5 Write property test for locked color preservation
    - **Property 4: Locked colors are preserved during generation**
    - **Validates: Requirements 2.2, 2.3**

- [x] 4. Implement contrast ratio calculations
  - [x] 4.1 Create contrast utility functions
    - Implement calculateContrastRatio using WCAG formula
    - Implement meetsWCAG_AA (ratio >= 4.5)
    - Implement meetsWCAG_AAA (ratio >= 7.0)
    - _Requirements: 6.1, 6.2_
  
  - [x] 4.2 Write property test for WCAG classification
    - **Property 16: WCAG classification is correct**
    - **Validates: Requirements 6.2**
  
  - [x] 4.3 Write unit tests for contrast calculations
    - Test known color pairs with expected ratios
    - Test black/white (21:1 ratio)
    - _Requirements: 6.1, 6.2_

- [x] 5. Implement URL state management
  - [x] 5.1 Create URL encoding and decoding functions
    - Implement encodePaletteToUrl (serialize palette to hash parameters)
    - Implement decodePaletteFromUrl (deserialize from URL)
    - Handle invalid/corrupted URLs gracefully
    - _Requirements: 5.1, 5.2_
  
  - [x] 5.2 Write property test for URL round-trip
    - **Property 13: URL encoding round-trip preserves palette**
    - **Validates: Requirements 5.1, 5.2**
  
  - [x] 5.3 Write unit tests for URL edge cases
    - Test malformed URLs
    - Test missing parameters
    - Test invalid color values
    - _Requirements: 5.1, 5.2_

- [x] 6. Create custom hooks for state management
  - [x] 6.1 Implement usePalette hook
    - Manage palette state (colors, locks, harmony rule)
    - Provide generatePalette function
    - Provide toggleLock function
    - Provide updateColor function
    - Load initial palette from URL or generate random
    - Sync palette changes to URL
    - _Requirements: 1.1, 1.2, 2.1, 2.2, 4.2, 5.2_
  
  - [x] 6.2 Implement useClipboard hook
    - Provide copyToClipboard function
    - Handle clipboard API availability
    - Return success/error state
    - _Requirements: 3.1_

- [x] 7. Build ColorSwatch component
  - [x] 7.1 Create ColorSwatch component with display and interactions
    - Display color with current format (HEX/RGB/HSL)
    - Show lock indicator when locked
    - Handle click to toggle lock
    - Handle click on value to copy to clipboard
    - Show hover state with adjustment controls
    - _Requirements: 2.1, 2.4, 3.1, 4.1_
  
  - [x] 7.2 Add color adjustment controls
    - Create sliders for hue (0-360), saturation (0-100), lightness (0-100)
    - Update color in real-time as sliders move
    - Auto-lock color when adjusted
    - _Requirements: 4.2, 4.3, 4.4_
  
  - [x] 7.3 Write property test for lock toggle
    - **Property 3: Lock toggle changes state**
    - **Validates: Requirements 2.1**
  
  - [x] 7.4 Write property test for lock indicator display
    - **Property 5: Lock state determines visual indicator**
    - **Validates: Requirements 2.4**
  
  - [x] 7.5 Write property test for auto-lock on adjustment
    - **Property 12: Manual adjustment auto-locks color**
    - **Validates: Requirements 4.3**

- [x] 8. Build ContrastIndicator component
  - [x] 8.1 Create ContrastIndicator component
    - Calculate contrast ratio between two colors
    - Display WCAG AA/AAA compliance badges
    - Show warning icon for insufficient contrast
    - Display numeric ratio on hover
    - _Requirements: 6.1, 6.2, 6.3, 6.4_
  
  - [x] 8.2 Write property test for contrast calculation completeness
    - **Property 15: Contrast ratios calculated for adjacent pairs**
    - **Validates: Requirements 6.1**
  
  - [x] 8.3 Write property test for warning display
    - **Property 18: Low contrast shows warning**
    - **Validates: Requirements 6.4**

- [x] 9. Build FormatSelector component
  - [x] 9.1 Create FormatSelector component
    - Radio buttons or toggle for HEX/RGB/HSL
    - Update global format state
    - _Requirements: 3.3_
  
  - [x] 9.2 Write property test for format consistency
    - **Property 8: Format selection updates all displays**
    - **Validates: Requirements 3.3**
  
  - [x] 9.3 Write property test for code-ready formatting
    - **Property 9: Color values are code-ready**
    - **Validates: Requirements 3.4**

- [x] 10. Build ExportButton component
  - [x] 10.1 Create ExportButton with share and download
    - Generate shareable URL (copy to clipboard)
    - Download palette as JSON file
    - Show copy confirmation message
    - _Requirements: 5.1, 5.3_
  
  - [x] 10.2 Write property test for JSON export completeness
    - **Property 14: JSON export contains all formats**
    - **Validates: Requirements 5.3, 5.4**

- [x] 11. Build PaletteDisplay component
  - [x] 11.1 Create PaletteDisplay component
    - Display all 5 ColorSwatch components in responsive grid
    - Display ContrastIndicator components between adjacent colors
    - Handle spacebar keypress for palette generation
    - Include generate button
    - _Requirements: 1.2, 6.1_
  
  - [x] 11.2 Write integration test for spacebar generation
    - Test keyboard event triggers new palette
    - _Requirements: 1.2_

- [x] 12. Build main App component and styling
  - [x] 12.1 Create App component with layout
    - Integrate PaletteDisplay, FormatSelector, ExportButton
    - Set up styled-components theme provider
    - Apply minimal, clean layout
    - _Requirements: 7.1_
  
  - [x] 12.2 Implement dynamic UI theming
    - Use current palette colors to style UI elements
    - Update styling when palette changes
    - Hide secondary controls when not interacting
    - _Requirements: 7.2, 7.3, 7.4_
  
  - [x] 12.3 Write property test for UI styling consistency
    - **Property 19: UI styling reflects current palette**
    - **Validates: Requirements 7.2, 7.4**
  
  - [x] 12.4 Write property test for control visibility
    - **Property 20: Controls hidden when not interacting**
    - **Validates: Requirements 7.3**

- [x] 13. Implement clipboard functionality across components
  - [x] 13.1 Wire up clipboard operations
    - Connect ColorSwatch copy-on-click to useClipboard hook
    - Connect ExportButton URL sharing to clipboard
    - Display confirmation messages
    - Handle clipboard errors gracefully
    - _Requirements: 3.1, 3.2, 5.1_
  
  - [x] 13.2 Write property test for clipboard operations
    - **Property 6: Clipboard receives correct color value**
    - **Validates: Requirements 3.1**
  
  - [x] 13.3 Write property test for copy confirmation
    - **Property 7: Copy action shows confirmation**
    - **Validates: Requirements 3.2**

- [x] 14. Add accessibility features
  - [x] 14.1 Implement accessibility enhancements
    - Add ARIA labels to all interactive elements
    - Add keyboard navigation support
    - Add focus indicators
    - Support prefers-reduced-motion
    - Make contrast warnings screen-reader accessible
    - _Requirements: 6.2, 6.3, 6.4_

- [x] 15. Polish and final integration
  - [x] 15.1 Add animations and transitions
    - Smooth color transitions when palette changes
    - Fade in/out for controls
    - _Requirements: 1.4_
  
  - [x] 15.2 Final integration and testing
    - Test complete user workflows
    - Verify all components work together
    - Test URL sharing end-to-end
    - Test on different browsers
    - _Requirements: All_

- [x] 16. Checkpoint - Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.
