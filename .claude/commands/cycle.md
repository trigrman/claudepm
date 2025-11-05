---
description: Start a new product discovery cycle with optional interview
---

You are being asked to start a new product discovery cycle for the NAM Demo application.

# Task

1. **Record start time**:
   - Capture the current timestamp as the operation start time
   - This will be used for timing metrics

2. **Get cycle information from user**:
   - Ask the user for the cycle name (short slug, e.g., "dark-mode", "notifications", "analytics")
   - Ask for a brief description of the feature/theme (one sentence)
   - Ask if they want to be interviewed to populate the baseline cycle context (yes/no)

3. **Create cycle directory structure**:
   - Generate cycle directory name: `{YYYY-MM-DD}-{cycle-name}` using today's date (ISO format)
   - Create directories using Bash tool:
     - `product/discovery/{cycle-date}/`
     - `product/discovery/{cycle-date}/interviews/`
     - `product/discovery/{cycle-date}/observations/`
   - Create initial README.md with template content:
     ```markdown
     # Discovery Cycle: {cycle-date}

     **Started**: {YYYY-MM-DD}
     **Focus**: {description}
     **Status**: Active

     ## Goals
     {description}

     ## Research Methods
     - [x] AI-guided stakeholder interview
     - [ ] Technical observations
     - [ ] Additional research as needed

     ## Timeline
     - **Start**: {YYYY-MM-DD}
     - **Target completion**: TBD
     - **Synthesis by**: TBD

     ## Key Decisions
     [To be documented during cycle]

     ## Notes
     [Context and findings]
     ```
   - Create `.synthesis-pending` marker file (empty file)
   - Copy interview template from `product/templates/interview-template.md` to `interviews/` directory if it exists

4. **Conduct interview (if user said yes)**:
   - If the user wants to be interviewed:
     - Conduct a structured discovery interview based on the cycle context
     - Ask about:
       - Business drivers and rationale for the feature
       - Target users and their pain points
       - Feature scope and requirements
       - Success metrics and goals
       - Timeline and dependencies
       - MVP scope (what's in, what's deferred)
     - Keep the interview conversational but comprehensive
     - Take notes during the interview

5. **Save interview notes (if interview was conducted)**:
   - Format the interview as a proper interview document
   - Include:
     - Interview metadata (date, participant, role, duration)
     - Key findings organized by topic
     - Direct quotes from the user
     - Insights and observations
     - Open questions
     - Tags
   - Save to `product/discovery/{cycle-date}/interviews/interview-{user-name}-{date}.md`
   - Use the interview template format from `product/templates/interview-template.md`

6. **Update cycle README**:
   - Update `product/discovery/{cycle-date}/README.md` with:
     - Specific goals for this cycle
     - Research methods used (interview, observations, etc.)
     - Key decisions made during setup
     - Timeline information
   - Keep it concise but informative

7. **Record timing and report results**:
   - Capture the end timestamp
   - Calculate duration in seconds
   - Create timing.json in the cycle directory:
     ```json
     {
       "cycle_name": "{cycle-date}",
       "operations": [
         {
           "command": "/cycle",
           "start": "{start_timestamp_ISO8601}",
           "end": "{end_timestamp_ISO8601}",
           "duration_seconds": {duration},
           "status": "success",
           "metadata": {
             "interview_conducted": true/false
           }
         }
       ],
       "total_duration_seconds": {duration}
     }
     ```
   - Append to global timing log at `artifacts/timing-log.jsonl`:
     ```json
     {"timestamp": "{end_timestamp}", "command": "/cycle", "cycle": "{cycle-date}", "duration_seconds": {duration}, "status": "success", "metadata": {"interview_conducted": true/false}}
     ```
   - Tell the user:
     - The cycle has been created
     - The cycle directory path
     - If interview was conducted, mention the interview notes location
     - The operation duration
     - Suggest next steps:
       - Add technical observations if needed
       - Run `/synth` when ready to synthesize
       - Or conduct additional interviews/research

# Notes

- The cycle name should be a short, hyphenated slug (e.g., "dark-mode", not "Dark Mode Feature")
- The description is just for context - keep it to one sentence
- The interview should be thorough but not exhausting - aim for 10-15 minutes worth of questions
- If the user declines the interview, just create the structure and they can add materials manually
- All directory and file creation is handled by the slash command using Bash and Write tools
- Interview questions should be tailored to the feature type (UI feature vs backend service vs infrastructure)
