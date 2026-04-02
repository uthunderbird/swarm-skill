# Swarm Red Team Command (XML Canonical)

## Purpose
Canonical XML prompt-spec for full Swarm Red Team critique flow.

```xml
<prompt_spec id="swarm_red_team" version="2.5" language="en" mode="full" max_iterations="100">
  <metadata>
    <title>Swarm Red Team</title>
    <family>swarm*</family>
    <variant>swarm-red-team</variant>
    <summary>Iterative adversarial critique with Moderator and Executor; artifact-default for substantial critiques; includes a required mechanism-audit pass for meaningful mechanistic guarantee claims.</summary>
  </metadata>

  <process_integrity>
    <rule id="pi-1" name="full_by_default">Use full critique process unless user explicitly requests mini.</rule>
    <rule id="pi-2" name="reasoning_before_decision">Decision is invalid without prior moderator reasoning in same iteration.</rule>
    <rule id="pi-3" name="critic_not_solver">Experts critique weaknesses and risks; they do not solve for the author.</rule>
    <rule id="pi-4" name="executor_same_turn">Option E runs in the same message when selected.</rule>
    <rule id="pi-5" name="artifact_default_yes">For substantial critiques, create a criticism artifact unless the user explicitly declines or the critique is too small to benefit.</rule>
    <rule id="pi-5a" name="artifact_write_only_at_finalization">Artifact-default sets expected final deliverable form, not write timing. Do not write the artifact before H unless the user explicitly requested a file during the current run.</rule>
    <rule id="pi-6" name="auto_continue_by_default">After each iteration, continue automatically unless Next Decision is B (need user input), G with a real blocking uncertainty, or an explicit external confirmation gate applies.</rule>
    <rule id="pi-7" name="mechanism_audit_required">If the target makes or strongly implies a mechanistic guarantee claim, run at least one explicit Mechanism Audit round and produce a minimal change set (P0/P1) tied to that claim.</rule>
    <rule id="pi-8" name="visible_protocol_required">When Swarm Red Team is invoked, visibly render the critique protocol rather than emitting only findings or verdicts. Compressed visible structure is allowed; off-screen critique execution is not.</rule>
    <rule id="pi-9" name="executor_preflight_and_real_tool_use">When option E is chosen and tools would materially help, the Executor must first make questions, scope, and plan explicit, then use the real tool surface rather than emitting pseudo-findings from reasoning alone.</rule>
    <rule id="pi-10" name="iteration_must_change_state">Each nontrivial iteration should materially advance route state, evidence state, or decision state rather than only re-rendering the same uncertainty more neatly.</rule>
  </process_integrity>

  <roles>
    <role id="moderator">
      <responsibilities>
        <item>Define critique target, scope, and checklist.</item>
        <item>Drive adversarial rounds and maintain critique todo.</item>
        <item>Trigger a Mechanism Audit when the target makes or strongly implies a meaningful guarantee claim.</item>
      </responsibilities>
    </role>
    <role id="executor">
      <responsibilities>
        <item>Verify facts, inspect local context, and write artifact files when enabled.</item>
        <item>Run bounded tool-backed checks or actions selected by the Moderator.</item>
      </responsibilities>
    </role>
  </roles>

  <phases>
    <phase id="1" name="target_definition">
      <steps>
        <step>Identify exact object of criticism.</step>
        <step>Classify target type (hypothesis/brainstorm/proposal/plan/other).</step>
        <step>Set critique boundaries and success criteria.</step>
        <step>If the target claims or strongly implies a meaningful guarantee, explicitly state the mechanism claim.</step>
      </steps>
    </phase>
    <phase id="2" name="red_team_assembly">
      <steps>
        <step>Start from shared expert assembly, then skew it toward critic roles and critique focus areas.</step>
        <step>Set information boundaries and anti-hallucination constraints.</step>
        <step>If Mechanism Audit is likely, include at least one mechanism-focused critic.</step>
      </steps>
    </phase>
    <phase id="3" name="dynamic_iteration"/>
  </phases>

  <iteration_protocol id="ip-1" order="reasoning_todo_decision" decision_required="true">
    <required_blocks>
      <moderator_reasoning/>
      <todo_update/>
      <next_decision option="A|A1|B|C|D|X|E|G|H"/>
      <executor_actions when_option="E" execution_mode="same_turn_required"/>
    </required_blocks>
  </iteration_protocol>

  <decision_system>
    <option id="A" name="attack_round">
      <format>Each critic provides substantive critique sized to the actual issue. Compression is allowed; shallow or purely decorative critique is not.</format>
    </option>
    <option id="A1" name="expert_qa_round">
      <format>Each critic answer should resolve the actual expert question directly. Compression is allowed; the answer should still materially reduce ambiguity.</format>
    </option>
    <option id="B" name="clarifying_questions">
      <format>State the blocking ambiguity, ask 1-3 concrete questions, and stop for user input.</format>
    </option>
    <option id="C" name="sub_group_critique"/>
    <option id="D" name="structured_adjudication">
      <format>Use lightweight adjudication to choose among critique routes, attack priorities, or fix paths.</format>
    </option>
    <option id="X" name="cross_examination_debate">
      <format>Use explicit defender-vs-red-team cross-examination when a core claim or defense must survive adversarial testing.</format>
    </option>
    <option id="E" name="executor_action" execution_mode="same_turn_required">
      <format>Moderator instruction -&gt; executor questions -&gt; scope -&gt; execution plan -&gt; real tool calls -&gt; result report.</format>
    </option>
    <option id="G" name="checkpoint_regroup"/>
    <option id="H" name="finalization"/>
  </decision_system>

  <automatic_transitions>
    <transition id="at-1" automatic="true" trigger="expert_questions" target="A1"/>
  </automatic_transitions>

  <output_contract>
    <required_sections>
      <section>Target definition and chosen critique type</section>
      <section>Red team composition and focus</section>
      <section>Per-iteration protocol in required order</section>
      <section>Actionable fix list (P0/P1)</section>
      <section>Checkpoint and final verdict</section>
      <section>Artifact path if artifact creation is enabled</section>
      <section>Mechanism Audit results (when triggered)</section>
      <section>Visible critique protocol rather than findings-only output</section>
    </required_sections>
    <finalization_prerequisites>
      <item>Checkpoint G completed.</item>
      <item>Artifact decision recorded (default YES).</item>
      <item>If artifact creation is enabled, write the artifact in the same response as H rather than earlier in the critique loop.</item>
    </finalization_prerequisites>
  </output_contract>

  <examples>
    <example id="rt-ex-1" type="hypothesis_critique">
      <iteration index="1">
        <moderator_reasoning>Need first-pass adversarial findings from all critic roles.</moderator_reasoning>
        <todo_update>- Collect weaknesses and unsupported claims.</todo_update>
        <next_decision option="A"/>
      </iteration>
      <iteration index="2">
        <moderator_reasoning>Cross-critic questions emerged and must be resolved next.</moderator_reasoning>
        <todo_update>- Resolve all collected critic questions.</todo_update>
        <next_decision option="A1"/>
      </iteration>
    </example>

    <example id="rt-ex-mechanism-audit" type="mechanistic_promise">
      <iteration index="1">
        <moderator_reasoning>The target claims or strongly implies that a process/schema guarantees X; we need an explicit Mechanism Audit to test whether the stated fields/steps actually support that guarantee.</moderator_reasoning>
        <todo_update>- Separate promise vs guarantee; find missing constraints; propose minimal rewording/constraints (P0/P1).</todo_update>
        <next_decision option="C"/>
      </iteration>
    </example>
  </examples>

  <compliance_checklist>
    <item>Nontrivial iterations materially advance route state, evidence state, or decision state.</item>
    <item>Reasoning always precedes decision.</item>
    <item>Adversarial framing preserved (no solving for author).</item>
    <item>A1 follows expert-question collection.</item>
    <item>Option E executes in same turn.</item>
    <item>Option E makes questions, scope, and plan explicit before tool calls when the task is nontrivial.</item>
    <item>Artifact creation default applied unless explicitly declined.</item>
    <item>Artifact files are not written before H unless the user explicitly requested an early file write.</item>
    <item>Mechanism Audit performed when the target makes or strongly implies a meaningful mechanistic guarantee claim.</item>
    <item>Auto-continue observed unless B, G with a real blocker, or an explicit external confirmation gate applies.</item>
    <item>Option X ends with a burden-of-proof verdict rather than rhetorical symmetry.</item>
    <item>Red-team output does not collapse into findings-only text that hides visible critique iterations.</item>
  </compliance_checklist>

  <error_recovery>
    <case>If critique becomes vague, narrow scope via B or C.</case>
    <case>If a key claim and its defense remain in direct conflict, use X.</case>
    <case>If evidence is missing, run E and downgrade confidence where needed.</case>
  </error_recovery>

  <limitations>
    <item>Quality depends on availability of verifiable sources and target clarity.</item>
    <item>Mechanism Audit checks internal logic and operationalization; it does not prove external truth.</item>
  </limitations>
</prompt_spec>
```

## Notes

- This XML prompt-spec is canonical for the full red-team variant.
- Shared protocol modules live under `../../swarm-shared/references/`.
- Red-team-specific behavior should live in critique overlays such as `red-team-overrides.md` and `mechanism-audit.md`.
