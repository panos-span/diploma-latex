BUILD = build
SRC = .
MAIN = main
PDF = $(BUILD)/$(MAIN).pdf

.PHONY: all prepare clean rebuild

all: $(PDF)
	cp $(PDF) $(MAIN).pdf

$(BUILD):
	mkdir -p $(BUILD)

prepare: $(BUILD)
	# Copy top-level source files
	cp $(SRC)/$(MAIN).tex $(BUILD)/
	cp $(SRC)/references.bib $(BUILD)/
	cp $(SRC)/used-packages.sty $(BUILD)/
	# Copy packages (style files)
	mkdir -p $(BUILD)/packages
	cp $(SRC)/packages/*.sty $(BUILD)/packages/
	# Copy chapter tree (preserve directory structure)
	mkdir -p $(BUILD)/chapters/0_before
	mkdir -p $(BUILD)/chapters/01_greek
	mkdir -p $(BUILD)/chapters/introduction
	mkdir -p $(BUILD)/chapters/background
	mkdir -p $(BUILD)/chapters/experiments
	mkdir -p $(BUILD)/chapters/results
	mkdir -p $(BUILD)/chapters/conclusion
	cp $(SRC)/chapters/0_before/*.tex $(BUILD)/chapters/0_before/
	cp $(SRC)/chapters/01_greek/*.tex $(BUILD)/chapters/01_greek/
	cp $(SRC)/chapters/introduction/*.tex $(BUILD)/chapters/introduction/
	cp $(SRC)/chapters/background/*.tex $(BUILD)/chapters/background/
	cp $(SRC)/chapters/experiments/*.tex $(BUILD)/chapters/experiments/
	cp $(SRC)/chapters/results/*.tex $(BUILD)/chapters/results/
	cp $(SRC)/chapters/conclusion/*.tex $(BUILD)/chapters/conclusion/
	# Copy images
	mkdir -p $(BUILD)/images
	-cp $(SRC)/images/* $(BUILD)/images/ 2>/dev/null || true
	# Copy tables
	-mkdir -p $(BUILD)/tables
	-cp $(SRC)/tables/* $(BUILD)/tables/ 2>/dev/null || true
	-mkdir -p $(BUILD)/tables_greek
	-cp $(SRC)/tables_greek/* $(BUILD)/tables_greek/ 2>/dev/null || true
	# Copy prompts
	-mkdir -p $(BUILD)/prompts
	-cp -r $(SRC)/prompts/* $(BUILD)/prompts/ 2>/dev/null || true

$(PDF): prepare
	cd $(BUILD) && \
	xelatex -interaction=nonstopmode $(MAIN).tex && \
	biber $(MAIN) && \
	xelatex -interaction=nonstopmode $(MAIN).tex && \
	xelatex -interaction=nonstopmode $(MAIN).tex

# Full clean rebuild — use this when references or packages change
rebuild: clean all

clean:
	rm -rf $(BUILD)
	rm -f $(MAIN).pdf
