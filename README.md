# R&D Figma MCP

## Summary of Figma MCP capabilities

> 💡 Must use the Figma Desktop app

- Helps developers generate code from selected frame by select a Figma frame and write a prompt.
- Extracts design content by pulling in variables, components, and layout data directly into the IDE. Useful for design systems and component-based workflows.
- Retrieves Make resource from Make files and provide them to the LLM as context. This can help as you move from prototype to production application.
- Keeps the design system components consistent with Code Connect by reusing the actual components. Code Connect keeps the generated code consistent with the codebase.

## Tools and prompts

By default, the generated code is **React + Tailwind** stack, but can be customizable.

### get_code:

Get code from Figma Selection

> 💡 We don’t have to paste links, just select the frame or component in Figma before prompting.

- Change framework and stack:
  - `generate my Figma selection in Twig/Liquid template`
  - `generate my Figma selection in plain HTML + CSS`
  - `generate my Figma selection in React + SCSS`
- Use your components:
  We can set up Code Connect for best code reuse results.
  - `generate my Figma selection using components from src/components/ui`
- Combine both:
  - `generate my Figma selection using components from src/components/ui and style with SCSS`

### get_variable_defs (local only)

Returns the variables and styles used in your Figma selection (such as colors, spacing, typography).

- List all tokens used:
  - `get the variables used in my Figma selection`
- Focus on a specific type:
  - `what color and spacing variables are used in my Figma selection?`
- Get both names and values:
  - `list the variable names and their values used in my Figma selection`

### **create_design_system_rules**

A tool for creating a rule file that provide agents with the right context to translate designs into high-quality, codebase-aware frontend code. It helps ensure alignment with your design system and tech stack, improving the relevance and accuracy of generated output.

> 💡 Run this tool and make sure the result is saved to the correct `rules/` or `instructions/` path so your agent can access it during code generation.

## How to get the best output

> Specify the exact tool you need in your prompt for best results

### Structure Figma design

1. **Use components with common UI parts for better reuse purpose**
2. **Link components to real code using Code Connect**
3. **Use Figma variables for tokens like spacing, color, radius, and typography**
4. **Name layers and components with clear semantic/intent-driven labels**
5. **Use Auto Layout to avoid absolute positioning**
6. **Use annotations and dev resources (coming soon) to convey design intent that’s hard to visualize from UI alone (how things behave and respond)**

### Write effective prompts to guide the AI

First, we should list out **what a good prompt can do**:

- Align the result with the right **framework or styling system**
- Align with **codebase conventions** (file structure, naming, layout)
- Generate code in the correct **file path** (like `src/pages`, `components/ui`)
- Add or modify code **inside existing files** instead of creating new ones
- Follow specific **layout systems** (flexbox, grid, absolute)

Some examples:

- `Generate React code from the selected Figma frame and style it with SCSS`
- `Implement the selected frame using Twig components`
- `Generate this using components from src/components/ui`
- `Add this component to src/components/marketing/PricingCard.tsx`
- `Implement this using our Stack layout component`

> 💡 The more specific your prompt, the better the output. The clearer your intent, the more likely you'll get exactly what you need.

### Add custom rules based on your design system

Check your IDE or MCP client's documentation for how to structure rules, and experiment to find what works best for your team.

Learn more at [https://developers.figma.com/docs/figma-mcp-server/add-custom-rules/](https://developers.figma.com/docs/figma-mcp-server/add-custom-rules/)

### Avoid selecting large, heavy frames

Break screens into smaller parts for faster, more reliable results.

Large selections can **slow the tools down**, **cause errors**, or result in **incomplete responses**, especially when there's too much context for the model to process. Instead:

1. Generate code for **smaller sections or individual components** (e.g. `Card`, `Header`, `Sidebar`)
2. **If it feels slow or stuck, reduce your selection size and try again**

> 💡 Revisit the basics if the output doesn’t look right or align with your system design:
>
> - how the Figma file is structured
> - how the prompt is written
> - and what context is being sent

_Retrieves from [https://developers.figma.com/docs/figma-mcp-server/](https://developers.figma.com/docs/figma-mcp-server/)_
