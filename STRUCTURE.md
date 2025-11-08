# vhdl-forge-3v0 Directory Structure

**Status:** Marker files created, ready for content migration

This document describes the complete directory structure for the standalone FORGE repository.

## Top-Level Structure

```
vhdl-forge-3v0/
├── .claude/                  # AI agents (FRONT AND CENTER)
├── docs/                     # Documentation
├── examples/                 # Complete FORGE examples
├── vhdl/                     # VHDL source code
├── cocotb_tests/             # CocoTB VHDL simulation tests
├── python/                   # Python source code
├── tests/                    # Python unit tests (pytest)
├── scripts/                  # Standalone scripts
├── README.md                 # Main introduction
├── CLAUDE.md                 # AI agent guide
├── llms.txt                  # Quick reference
├── LICENSE
└── pyproject.toml
```

## Key Design Decisions

### 1. Agents Front and Center (`.claude/`)
- Entry point for AI-assisted development
- 4 specialized agents for autonomous VHDL workflow
- Each agent has README.md + agent.md

### 2. Clear Test Separation
- `cocotb_tests/` - VHDL simulation (CocoTB + GHDL)
- `tests/` - Python unit tests (pytest)
- **No confusion** about test runners or test types

### 3. Python Source Organization (`python/`)
- `forge_cocotb/` - CocoTB testing framework
- `forge_platform/` - Platform backend abstraction
- `forge_tools/` - Standalone utilities (HVS decoder, etc.)

### 4. VHDL Components (`vhdl/`)
- `packages/` - Core packages (FORGE control, serialization, voltage)
- `components/` - Reusable components (debugging, utilities, loader)
- **NO test_wrappers** in vhdl/ (moved to cocotb_tests/)

### 5. Documentation Hierarchy
- `README.md` - Human-oriented introduction
- `llms.txt` - Quick reference for AI agents
- `CLAUDE.md` - Complete AI development guide
- `docs/` - Detailed documentation (FORGE convention, HVS, architecture)

### 6. Example-Driven Learning (`examples/`)
- `counter/` - THE canonical FORGE example
- Includes HVS encoding (batteries included)
- Self-contained with VHDL + CocoTB tests

## README.md Coverage

Every directory has a README.md explaining its contents:

### Top-Level READMEs
- ✅ `/README.md` - Project introduction, quick start
- ✅ `/.claude/README.md` - Agent workflow overview
- ✅ `/docs/README.md` - Documentation index
- ✅ `/examples/README.md` - Examples catalog

### VHDL READMEs
- ✅ `/vhdl/README.md` - VHDL components overview
- ✅ `/vhdl/packages/README.md` - Package catalog
- ✅ `/vhdl/components/README.md` - Component catalog
- ✅ `/vhdl/components/debugging/README.md` - HVS encoder
- ✅ `/vhdl/components/utilities/README.md` - Utilities
- ✅ `/vhdl/components/loader/README.md` - BRAM loader (future)

### Testing READMEs
- ✅ `/cocotb_tests/README.md` - CocoTB testing guide
- ✅ `/cocotb_tests/components/README.md` - Component test structure
- ✅ `/cocotb_tests/platform/README.md` - Platform test patterns
- ✅ `/cocotb_tests/cocotb_test_wrappers/README.md` - Wrapper explanation
- ✅ `/tests/README.md` - Python pytest guide

### Python READMEs
- ✅ `/python/README.md` - Python packages overview
- ✅ `/python/forge_cocotb/README.md` - CocoTB framework
- ✅ `/python/forge_platform/README.md` - Platform backends
- ✅ `/python/forge_tools/README.md` - Utilities and decoders

### Other READMEs
- ✅ `/scripts/README.md` - Standalone scripts
- ✅ `/examples/counter/README.md` - Counter tutorial

## Special Note: cocotb_test_wrappers

Changed from `test_wrappers/` to `cocotb_test_wrappers/` per user request.

Location: `cocotb_tests/cocotb_test_wrappers/`

Purpose: VHDL wrappers for testing packages (CocoTB can't test packages directly).

## Next Steps

1. ✅ Directory structure created
2. ✅ README.md files at each level
3. ⏳ Review structure with user
4. ⏳ Migrate content from libs/forge-vhdl
5. ⏳ Update pyproject.toml
6. ⏳ Update llms.txt and CLAUDE.md
7. ⏳ Create docs/ content (FORGE_CALLING_CONVENTION.md, HVS_ENCODING.md, etc.)

## Migration Checklist (Future)

### From `libs/forge-vhdl/` to `vhdl-forge-3v0/`

**VHDL Files:**
- [ ] `vhdl/packages/*.vhd` → `vhdl/packages/`
- [ ] `vhdl/debugging/*.vhd` → `vhdl/components/debugging/`
- [ ] `vhdl/utilities/*.vhd` → `vhdl/components/utilities/`
- [ ] `vhdl/loader/*.vhdl` → `vhdl/components/loader/`

**CocoTB Tests:**
- [ ] `cocotb_test/test_duts/forge_counter_with_encoder.vhd` → `examples/counter/vhdl/`
- [ ] `cocotb_test/test_platform_counter_poc.py` → `examples/counter/cocotb_tests/`
- [ ] `cocotb_test/forge_*_tests/` → `cocotb_tests/components/*/`
- [ ] `cocotb_test/*_tb_wrapper.vhd` → `cocotb_tests/cocotb_test_wrappers/`
- [ ] `cocotb_test/platform/` → `cocotb_tests/platform/` (keep structure)

**Python Code:**
- [ ] `forge_cocotb/*.py` → `python/forge_cocotb/`
- [ ] `cocotb_test/platform/*.py` → `python/forge_platform/`
- [ ] Add HVS decoder → `python/forge_tools/hierarchical_decoder.py`

**Agents:**
- [ ] `.claude/agents/*` → `.claude/agents/`
- [ ] `.claude/forge-*.md` → `.claude/`

**Documentation:**
- [ ] `docs/VHDL_CODING_STANDARDS.md` → `docs/`
- [ ] `docs/COCOTB_TROUBLESHOOTING.md` → `docs/`
- [ ] Create `docs/FORGE_CALLING_CONVENTION.md` (from BPD FORGE_ARCHITECTURE.md)
- [ ] Create `docs/HVS_ENCODING.md` (from Obsidian/HVS.md)
- [ ] Create `docs/THREE_LAYER_ARCHITECTURE.md`
- [ ] Create `docs/GETTING_STARTED.md`

**Configuration:**
- [ ] Update `pyproject.toml` (workspace → standalone project)
- [ ] Update `llms.txt` (adapt for standalone context)
- [ ] Update `CLAUDE.md` (adapt for standalone context)

---

**Created:** 2025-11-08
**Status:** Structure ready for review
