# Recommendation: Integrating Claude AI into BYU Computer Science Upper-Division Curriculum

**Prepared for:** BYU Department of Computer Science
**Date:** January 2026
**Target Implementation:** Fall 2026

## Executive Summary

This document recommends the integration of Claude AI (Anthropic's AI assistant) into upper-division computer science courses at Brigham Young University, with a focus on software engineering and AI/ML coursework. The goal is to prepare students for professional software development in an AI-augmented workplace while maintaining academic integrity and ensuring fundamental skill development.

**Key Recommendation:** Implement a structured, pedagogy-first approach to Claude integration that treats AI as a professional development tool rather than a replacement for learning, with clear usage guidelines, assessment redesign, and faculty support.

## Rationale and Context

### Industry Reality

- By 2026, AI coding assistants are standard tools in professional software development
- Employers expect graduates to work effectively with AI tools, not in isolation from them
- Students graduating without AI tool experience will be at a competitive disadvantage

### Current State at BYU

- Faculty are already experimenting with AI tool integration in individual courses
- Students are using AI tools informally without consistent guidance
- The department has an opportunity to lead rather than react to AI adoption

### Target Courses

The initial implementation focuses on three courses where AI integration has clear pedagogical value:

**CS 260: Web Programming**

- Web development is one of the domains most transformed by LLM capabilities
- Students need to learn professional web development in an AI-augmented context
- Course instructor is enthusiastic about Claude integration
- Large enrollment makes this high-impact for student preparation

**CS 340: Software Design & CS 329: QA and DevOps**

- Upper-division courses where students have foundational programming skills established
- Course content (software architecture, testing, deployment) mirrors professional workflows
- Projects are complex enough to benefit from AI collaboration while testing design thinking
- Students are closer to industry transition and need professional tool experience

## Benefits of Structured Claude Integration

### For Students

**Professional Preparation**

- Experience using AI tools in controlled, educational settings before employment
- Learn to prompt effectively, verify AI outputs, and maintain code quality with AI assistance
- Develop critical evaluation skills for AI-generated code and architectural suggestions

**Enhanced Learning Opportunities**

- Access to on-demand code reviews and debugging assistance outside class hours
- Ability to explore unfamiliar technologies and frameworks more independently
- Exposure to different problem-solving approaches and design patterns

**Improved Project Outcomes**

- Students can tackle more ambitious projects with AI support for scaffolding and boilerplate
- More time for high-level design thinking rather than syntax debugging
- Better documentation and code quality through AI-assisted reviews

### For Faculty

**Better Assessment of Understanding**

- Move from "can students write code" to "can students architect systems, make design tradeoffs, and verify solutions"
- Focus on higher-order thinking skills that AI cannot replace
- Opportunity to redesign assessments for the AI era

**Enhanced Course Content**

- Cover more advanced topics when students can use AI for foundational scaffolding
- Incorporate industry-relevant workflows and tools
- Teach critical AI literacy alongside technical skills

### For the Department

**Academic Leadership**

- Position BYU CS as a forward-thinking department preparing students for modern software development
- Develop best practices that can be shared with other institutions
- Attract students interested in cutting-edge educational approaches

**Research Opportunities**

- Generate publishable insights on AI-assisted CS education
- Contribute to understanding of effective AI pedagogy
- Potential for external funding focused on AI in education

## Recommended Approach

### Core Principle: Transparent, Pedagogically-Grounded Integration

Claude should be integrated as a **transparent professional tool** with clear usage guidelines, not banned or left ambiguous. The approach has three pillars:

### 1. Clear Usage Framework

Establish three tiers of Claude usage across assignments:

**Tier 1: Collaborative Work (Claude Encouraged)**

- Design discussions and architectural decisions
- Code review and refactoring exercises
- Learning new frameworks or tools
- Debugging and problem diagnosis
- Documentation and code explanation

**Tier 2: Guided Assistance (Claude Allowed with Attribution)**

- Implementation of non-core features
- Boilerplate and scaffolding code
- Test case generation
- Research of APIs and libraries
- Students must document what Claude generated and verify correctness

**Tier 3: Individual Assessment (Claude Prohibited)**

- Core algorithm implementation demonstrating understanding
- Timed assessments of fundamental skills
- Specific "prove you can do this" exercises
- Students must complete these independently to demonstrate mastery

Each assignment should clearly state which tier applies and why.

### 2. Redesigned Assessments

Move beyond "can you write this code" to "can you solve this problem":

**Process Documentation**

- Require students to document their problem-solving process, design decisions, and how they used Claude
- Assess reasoning and decision-making, not just final code

**Design-First Assignments**

- Focus on system architecture, API design, and tradeoff analysis
- AI can help with implementation, but students must justify design choices

**Code Review and Verification**

- Give students AI-generated code and ask them to review, test, and improve it
- Assess their ability to evaluate and fix AI outputs

**Oral Examinations/Demos**

- Short one-on-one discussions where students explain their code and design decisions
- Difficult to fake understanding in conversation

**Comparative Analysis**

- Ask students to generate multiple solutions (including with Claude) and analyze tradeoffs
- Assess critical thinking about different approaches

### 3. Explicit Skill Development

Integrate "working with AI" as a learning outcome:

**Prompt Engineering**

- Teach effective questioning and context provision
- Show how to iterate on AI responses

**Verification and Testing**

- Emphasize that AI output must be verified, not trusted blindly
- Teach code review skills using AI-generated code

**AI Limitations**

- Discuss where AI excels (boilerplate, common patterns) and where it fails (novel algorithms, complex reasoning)
- Use AI failures as teaching moments

### 4. Autograding for Understanding at Scale

**The Reality:** With 1,500 students and 40 faculty, manual grading of every assignment is impossible. Autograders are essential infrastructure.

**The Challenge:** Traditional autograders test correctness (does the code produce the right output?), not understanding. In the AI era, students can generate correct code without understanding it.

**The Solution:** Evolve autograders to assess understanding, design decisions, and code quality - not just functional correctness.

#### Autograding Strategies for AI-Era Assessment

**1. Multi-Dimensional Autograding**

Don't just test if code works - test HOW it works:

```
Traditional Autograder:
✓ Does function return correct output for test cases?

AI-Era Autograder:
✓ Does function return correct output?
✓ Does code follow required architectural constraints?
✓ Are there comprehensive tests with good edge case coverage?
✓ Is code documented with design decisions explained?
✓ Does code meet performance requirements?
✓ Are there any code quality issues (security, efficiency)?
```

**2. Constraint-Based Assessment**

Require specific implementation approaches that demonstrate understanding:

- "Implement using recursion (no loops allowed)" - tests recursive thinking
- "Use only functional programming patterns" - tests understanding of paradigms
- "Must handle errors using Result/Either types" - tests error handling design
- "Implement without using library X" - tests algorithmic understanding
- "Optimize for O(n log n) time complexity" - tests algorithm analysis

Students can use Claude to help, but must meet constraints that require understanding.

**3. Code Explanation Requirements**

Autograders can validate that students submit explanations alongside code:

- Require comments explaining design decisions (autograder checks for presence and quality)
- Require README documenting approach and tradeoffs
- Use LLM-based autograding to assess explanation quality (does explanation match code?)
- Award partial credit only if explanation demonstrates understanding

**4. Test-Driven Requirements**

Require students to write comprehensive tests first:

- Autograder evaluates test quality (edge cases, coverage, assertions)
- Students must write tests before implementation
- Claude can help implement, but students must demonstrate testing understanding
- Good tests indicate understanding of requirements and edge cases

**5. Comparative Implementation**

Ask students to submit multiple solutions:

- "Submit both an O(n²) and O(n log n) solution and explain the tradeoff"
- "Implement using both iterative and recursive approaches"
- "Provide both a simple and an optimized version"

Autograder checks that both exist and students explain the differences.

**6. Code Review and Debugging Assignments**

Give students BROKEN or SUBOPTIMAL code to fix:

- Autograder provides intentionally flawed code
- Students must identify issues, explain what's wrong, and fix it
- Tests understanding and code review skills, not just generation
- Claude can help, but students must articulate the problems

**7. Design Document Requirements**

Require design artifacts before code submission:

- Submit architecture diagram or pseudocode first (manual or automated review)
- Implementation must match approved design
- Autograder validates alignment between design and code
- Separates planning (high-order thinking) from implementation (AI-assistable)

#### Course-Specific Autograding Examples

**CS 260: Web Programming**

```
Assignment: Build a full-stack task management app

Autograder checks:
- Functional correctness (features work as specified)
- REST API follows standard conventions (proper HTTP methods, status codes)
- Database schema is normalized (no obvious redundancy)
- Frontend uses modern component architecture
- Accessibility requirements met (semantic HTML, ARIA labels)
- Security basics (input validation, SQL injection prevention)
- Comprehensive tests for API endpoints
- README explains architecture decisions

Students can use Claude to generate boilerplate, but must make and explain design decisions.
```

**CS 340: Software Design**

```
Assignment: Design and implement a plugin architecture for [system]

Autograder checks:
- System follows specified design pattern (Strategy, Observer, etc.)
- Interfaces properly define contracts
- Plugins can be added without modifying core system (Open/Closed Principle)
- Design document explains pattern choice and tradeoffs
- Unit tests demonstrate plugin isolation
- Code includes example plugins showing extensibility

AI can assist with implementation, but design decisions must be justified.
```

**CS 329: QA and DevOps**

```
Assignment: Create CI/CD pipeline with comprehensive testing

Autograder checks:
- Pipeline successfully builds, tests, and deploys
- Multiple types of tests present (unit, integration, E2E)
- Test coverage meets threshold (e.g., 80%)
- Performance tests validate response time requirements
- Static analysis tools integrated (linting, security scanning)
- Pipeline fails appropriately when tests fail
- Documentation explains testing strategy and tool choices

Claude can help configure tools, but students must understand testing strategy.
```

#### Implementing LLM-Assisted Autograding

**Use Claude API for Automated Assessment:**

Autograders can themselves use Claude to evaluate subjective criteria:

```python
def assess_code_explanation(code, explanation):
    """Use Claude API to evaluate if explanation demonstrates understanding."""
    prompt = f"""
    Evaluate if this student explanation demonstrates genuine understanding:

    CODE:
    {code}

    STUDENT EXPLANATION:
    {explanation}

    Rate 1-5 and explain:
    1 = Generic/AI-generated explanation, no real understanding
    3 = Basic understanding but missing depth
    5 = Clear demonstration of design thinking and tradeoffs
    """

    # Call Claude API
    response = claude_api.complete(prompt)
    return parse_score_and_feedback(response)
```

This allows scalable evaluation of understanding, not just correctness.

#### Key Principle: Correctness is Baseline, Understanding is the Goal

**Traditional grading:** 100% of points for correct output
**AI-era grading:**

- 40% Functional correctness (does it work?)
- 20% Design quality (is it well-architected?)
- 20% Testing and documentation (is it professional?)
- 20% Explanation and understanding (can student defend choices?)

This approach:

- Makes autograding feasible at scale (1,500 students)
- Tests understanding, not just code generation
- Allows Claude usage while ensuring learning
- Prepares students for professional development practices

## Addressing Department Concerns

### Concern 1: Academic Integrity and Cheating

**The Problem:** Students might use Claude to complete assignments without learning.

**The Solution:**

- **Leverage autograding for understanding:** As detailed in Section 4, autograders can test design quality, explanation, testing, and documentation - not just correctness. Students can't fake understanding across multiple dimensions.
- **Reframe the problem:** If an AI can trivially complete an assignment and pass the autograder, the assignment tests outdated skills. Multi-dimensional autograding makes this much harder.
- **Make AI use part of learning:** Explicitly teach students when and how to use AI appropriately in professional contexts. Include "effective AI collaboration" as a learning outcome.
- **Honor Code integration:** Include AI usage policies in course honor code discussions. BYU students respond well to clear expectations and integrity frameworks. Frame AI use as professional skill development, not cheating.
- **Process over product:** Require documentation of problem-solving process, not just final code. Autograders can validate explanation quality at scale using LLM-based assessment.
- **Constraint-based assignments:** Use implementation constraints (recursion-only, specific patterns, performance requirements) that require understanding to satisfy.

**Example:** Instead of "implement a binary search tree" (easily AI-generated), assign:

- "Implement both BST and AVL tree for [use case]"
- "Write comprehensive tests demonstrating tree properties"
- "Submit README explaining when to use each, with time/space analysis"
- "Autograder checks: correctness + test quality + explanation quality + performance constraints"

Students can use Claude for implementation help, but must demonstrate multi-dimensional understanding. Autograder can assess all dimensions at scale.

### Concern 2: Fundamental Skill Development

**The Problem:** Students might not develop core programming skills if they rely on AI.

**The Solution:**

- **Target upper-division courses:** Fundamental skills (loops, conditionals, basic algorithms) are taught in lower-division courses without AI assistance.
- **Tiered assignments:** Include explicit "no AI" components for core competencies that students must demonstrate independently.
- **Skills assessment:** Implement periodic practical exams or checkpoints where students demonstrate fundamental abilities without AI.
- **Progressive scaffolding:** Early in semester, limit AI use; increase allowance as students demonstrate core competence.
- **Focus on AI-resistant skills:** Emphasize system design, architecture, debugging reasoning, and critical evaluation—skills AI supports but doesn't replace.

**Example:** In a software engineering course, students might build a web application where:

- Weeks 1-3: Core architecture and data model designed independently
- Weeks 4-8: Implementation with Claude assistance allowed
- Week 9: Timed practical exam implementing a new feature without AI
- Final project: Full AI collaboration allowed, but oral defense required

### Concern 3: Cost and Access Equity

**The Problem:** AI tools cost money, and not all students can afford subscriptions.

**The Solution:**

- **Department licenses:** With budget allocated, purchase Claude Team or Enterprise licenses for all students in participating courses.
- **Academic pricing:** Anthropic offers educational discounts and may provide free or reduced-cost access for classroom use.
- **Free tier sufficiency:** For pilot programs, Claude's free tier provides substantial capability. Design assignments that work within free tier limits.
- **Computer lab access:** Ensure computer labs have Claude access for students who need it.
- **Transparency:** Make clear which features require paid vs. free tier and ensure course requirements work with free access.

**Budget Guidance:**

- Claude Pro: $20/month per student (if students pay individually)
- Claude Team: ~$30/month per seat (department purchase, better for classroom use)
- Claude Enterprise: Custom pricing for larger deployments
- For 100 students in upper-division courses: ~$3,000/month or ~$9,000 for a semester
- Alternative: Negotiate annual educational license for department

### Concern 4: Faculty Training and Adoption

**The Problem:** Faculty may not feel prepared to teach with AI tools or redesign their courses.

**The Solution:**

- **Faculty workshops:** Pre-semester training on Claude capabilities, pedagogical approaches, and assessment redesign.
- **Peer learning community:** Create faculty working group to share experiences and best practices.
- **Course redesign support:** Provide dedicated time/resources for faculty to redesign assessments and assignments.
- **Template assignments:** Develop shared assignment templates and rubrics that incorporate AI appropriately.
- **Gradual adoption:** Start with volunteer faculty in pilot courses, expand as comfort grows.
- **Ongoing support:** Designate an AI pedagogy coordinator to support faculty throughout the semester.

**Recommended Support:**

- Summer 2026 workshop series (3-4 sessions)
- Shared repository of AI-friendly assignments and rubrics
- Regular faculty check-ins during Fall 2026 semester
- Guest speakers from industry on AI-augmented development
- Budget for course release time or summer stipends for course redesign

## Implementation Scope for Fall 2026

### Target Courses for Initial Rollout

Based on department priorities and faculty readiness, the Fall 2026 launch will target three courses:

**CS 260: Web Programming**

- **Why:** Web development is heavily penetrated by LLMs; students need AI-assisted web dev skills for industry
- **Instructor enthusiasm:** Course instructor is eager to pilot Claude integration
- **High impact:** Large enrollment course reaching many students
- **Use cases:** HTML/CSS/JavaScript scaffolding, framework learning, API design, full-stack architecture, debugging browser issues
- **Assessment:** Autograder tests API design, accessibility, security basics, testing, and architectural documentation

> [!NOTE]
>
> `LEE` We have to be careful with 260 to make sure they don't just create their entire creative work with AI and not understand what they are doing. That is certainly possible and would basically be wasting their time. What I would like to do here is to start with **level 1** and use AI to accelerate their learning by giving them an AI tutor and small interactive exercises where they can get feedback from AI. Then move to **level 2** where the AI gives feedback on their design, code, and architecture. Finally you could do level 3 where they code with AI. Perhaps as a midterm or final where they have to build a specific website in a limited amount of time. AI would then verify that the website works and give them a grade. This could be contested and graded by a TA.

**CS 340: Software Design**

- **Why:** Core upper-division course focusing on design patterns, architecture, and software quality
- **Professional relevance:** Mirrors industry use of AI for design discussion and code review
- **Use cases:** Design pattern implementation, architecture discussions, code refactoring, UML diagram generation, design tradeoff analysis
- **Assessment:** Autograder validates pattern adherence, design documentation, extensibility, and justification of choices

**CS 329: Quality Assurance and Developer Operations**

- **Why:** QA and DevOps workflows naturally incorporate automation and AI-assisted tooling
- **Professional preparation:** CI/CD and testing are areas where AI tools are rapidly adopted in industry
- **Use cases:** Test case generation, CI/CD pipeline configuration, automated testing strategies, deployment scripting, monitoring setup
- **Assessment:** Autograder checks pipeline functionality, test coverage, quality metrics, and documented testing strategy

> [!NOTE]
>
> `LEE` Testing in 329 could really benefit from AI. I worry about complex CI pipelines. There is so much context that is outside of the Agent that it might cause more problems than it is worth unless the learner already knows what they are doing.
>
> 329 could also use AI as an introduction to agentic programming. For example, we could use MCP to give access to the observability logs to do automatic detection of anomalies.

**Rationale for Course Selection:**

- Mix of web development (CS 260) and software engineering fundamentals (CS 340, CS 329)
- Courses with enthusiastic faculty ready to pilot new approaches
- All three courses involve substantial projects where AI assistance mirrors professional workflows
- Combined enrollment provides significant student impact while remaining manageable for pilot
- Content naturally aligns with industry use of AI development tools

### Expected Student Impact

- Approximately 200-300 upper-division students across target courses
- All students receive clear guidance on AI tool usage in professional contexts
- Students graduate with practical experience using industry-standard AI assistants
- Improved job placement outcomes and employer satisfaction

## Success Criteria

### Student Outcomes

- Students can articulate when and how to use AI tools appropriately in software development
- Students demonstrate ability to verify and improve AI-generated code
- Students show strong performance on both AI-assisted and independent assessments
- Exit surveys show high satisfaction and perceived value of AI tool experience

### Faculty Outcomes

- Faculty report confidence in teaching with AI tools
- Assessment redesigns successfully measure student understanding
- Academic integrity incidents related to AI use are minimal
- Faculty identify opportunities to cover more advanced content

### Department Outcomes

- BYU CS develops replicable model for AI integration in CS education
- Department publishes or presents findings on AI pedagogy
- Student recruitment and placement outcomes improve
- Positive attention from industry partners and peer institutions

## Conclusion

Integrating Claude into upper-division CS courses represents a strategic investment in student preparation for professional software development. With careful pedagogical design, clear policies, adequate faculty support, and redesigned assessments, BYU CS can lead in preparing students for AI-augmented development while maintaining academic rigor and integrity.

The key is to treat AI integration not as a threat to learning, but as an opportunity to teach higher-order skills that will matter throughout students' careers: system design, critical evaluation, effective collaboration with AI tools, and principled decision-making in complex technical contexts.

**Next Steps:** See accompanying Implementation Plan for detailed timeline and action items for Fall 2026 launch.
