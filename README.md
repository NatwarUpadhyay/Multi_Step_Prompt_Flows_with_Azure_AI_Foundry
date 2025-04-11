# Multi_Step_Prompt_Flows_with_Azure_AI_Foundry



# Multi-Step Prompt System with Azure OpenAI

This repository demonstrates **Series** and **Parallel** Prompt Flows using Azure OpenAI. The included images show real-world implementations.  
**Renamed image files**:  
1. `parallel_flow_output.jpeg` - Final output of Parallel Flow (Product Launch Strategy)  
2. `parallel_flow_config.jpeg` - Parallel Flow configuration  
3. `series_flow_output.jpeg` - Series Flow output (Netflix Campaign)  
4. `series_flow_config.jpeg` - Series Flow design and configuration  

---

## 📋 Overview
- **Series Flow**: Sequential execution (e.g., Netflix campaign theme → timeline → activities).  
- **Parallel Flow**: Simultaneous input processing (e.g., combining TMA, MC, and PDS).  

---

## ⚙️ Prerequisites
- Azure OpenAI access (GPT-4/3.5).  
- Azure Machine Learning workspace.  
- Python SDK for Azure ML (`azure-ai-ml`).  

---

## 🔄 Series Prompt Flow
### Use Case: Netflix Marketing Campaign  
**Objective**: Generate a multi-phase campaign from a theme.  
**Steps** (matching `series_flow_config.jpeg`):  
1. **Input**: `topic = "Netflix"`.  
2. **Flow**:  
   - Step 1: Create campaign theme (`CampaignTheme`).  
   - Step 2: Build timeline (`CampaignTimeline`).  
   - Step 3: Design activities (`SampleActivity`).  
3. **Output** (from `series_flow_output.jpeg`):  
   ```text
   Campaign Timeline: "Unlimited Worlds, One Ticket"
   Activities: Multi-channel ads, influencer partnerships, analytics tracking.

⇶ Parallel Prompt Flow
Use Case: Product Launch Strategy

Objective: Combine TMA, MC, and PDS into a unified strategy.
Steps (matching parallel_flow_config.jpeg):

    Inputs:

        TMA: Target market analysis.

        MC: Marketing campaign ideas.

        PDS: Pricing/distribution strategy.

    Flow:

        Process inputs in parallel.

        Aggregate results into Final LLM.

    Output (from parallel_flow_output.jpeg):
    text
    Copy

    Actionable Strategy: 
    - Pricing: Premium model with early-access tiers.
    - Distribution: Online-first rollout.
    - Campaign: #TheNextBigThing teasers.

📂 Image Guide
Filename	Description
parallel_flow_output.jpeg	Final output of Parallel Flow (Product Launch Strategy).
parallel_flow_config.jpeg	Parallel Flow configuration with TMA/MC/PDS inputs.
series_flow_output.jpeg	Series Flow output (Netflix campaign timeline).
series_flow_config.jpeg	Series Flow design with step chaining.
🛠️ Implementation

    Series Flow Setup (see series_flow_config.jpeg):
    yaml
    Copy

    steps:
      campaign_theme:
        component: azureml:LLM_CampaignTheme
      campaign_timeline:
        component: azureml:LLM_Timeline
        inputs:
          theme: ${{steps.campaign_theme.outputs.theme}}

    Parallel Flow Setup (see parallel_flow_config.jpeg):
    yaml
    Copy

    inputs:
      - name: TMA
        type: string
      - name: MC
        type: string
      - name: PDS
        type: string
    steps:
      final_strategy:
        component: azureml:LLM_FinalStrategy
        inputs:
          tma: ${{inputs.TMA}}
          mc: ${{inputs.MC}}
          pds: ${{inputs.PDS}}

📚 Resources

    Azure Prompt Flow Documentation

    AML Python SDK Guide
