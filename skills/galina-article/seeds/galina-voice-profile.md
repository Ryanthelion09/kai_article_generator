---
name: galina-voice-profile
description: Stylometric markers of Galina Antova's writing voice, drawn from her Dark Reading, Fortune, Forbes, and kai.security pieces
metadata:
  type: reference
---

Observed from "Rethinking Vulnerability Disclosures In ICS" (Dark Reading), "As the red line disappears" (Fortune), "Building A New Product Category" (Forbes), and "We Aren't Building a Better Tool. We're Rebuilding Security." (kai.security, 2026) — the reference samples bundled with this skill in `${CLAUDE_SKILL_DIR}/galina/`.

**Tone & register:** Confident, declarative, operator-authoritative but not stuffy. Warm-but-direct. Speaks from lived experience ("In my case," "we've seen," "we need to"). Writes as an insider correcting the industry's bad habits.

**Openers:** Frames a structural shift up front with a short punchy declarative. E.g. "The red lines once thought to be unapproachable... have dimmed significantly." She likes the "that world is gone" move — establish old reality, declare it over.

**Rhetorical questions as pivots:** Heavy, characteristic. Uses them as section turns and to puncture pace: "Why?", "When will it be enough? Where is the red line?", "What's Patching?". Often answers immediately. This fits GEO question-form subheads naturally.

**Signature devices/idioms:** vivid plain-language metaphors — "boiling frog," "double-edged sword," "a gazillion ways to get in," "the bad guys," "downtime = no good for business = no patching" (uses the = construction for emphasis). Em-dashes and parentheticals throughout. Contractions used freely.

**Her actual sign-off:** literally writes "Bottom line:" to close (Dark Reading). So a GEO "Bottom line" block is on-brand, not a tic to remove.

**Core recurring thesis / worldview:** systemic over sensational — don't chase headlines/hype, fix the structural problem. "You cannot protect what you cannot see" is her signature ICS line (visibility/asset inventory before patching). The disclose-and-patch cycle fails without a known inventory — she made this exact argument about ICS in 2017. Maps perfectly onto SBOM/dependency-chain arguments.

**Structure:** Prescriptive numbered lists with bolded lead-ins ("1. Identify the changing assumptions."), each followed by a "takeaway" sentence. Data-driven: cites a named source + specific stat early and often, woven into prose not dumped.

**Manifesto register (kai.security sample — a third gear, for vision pieces only):** opens with an aphorism stated as conviction ("You cannot win a machine-speed war with human-speed defenses."); very short declaratives and deliberate fragments; "X isn't Y. It's Z." reframes ("Kai is not a tool. It's an agentic AI platform…", "This isn't an upgrade. It's a rebuild."); anaphoric runs ("Replacing the fragmented stack. Eliminating the manual workflows. Ending the broken handoffs…"); a recurring refrain ("we're just getting started", used 3x); customer/CISO quotes doing the evidentiary work instead of statistics; subheads as full claims ("A Failure of Imagination", "The Real Problem Isn't the Tools. It's the Model in Which the Tools Fit."). Don't flag these devices as off-voice in vision/announcement pieces — but they'd be drift in an advice column or argued op-ed.

**Common drift in generated drafts to fix:** prose can be too neutral/consultant-flat, over-hedged, or lack her idioms and first-person operator voice. Inject: a crisp declarative opener, a rhetorical-question pivot, one vivid plain-language metaphor, and an explicit callback to her "can't protect what you can't see / inventory-before-patching" worldview when topically relevant.
