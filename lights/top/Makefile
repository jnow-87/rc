# to test
# 	rpm
# 	feedrate
# 	diameter
# 	isolation with

# commands
quiet := $(if $V,,@)

rm := $(quiet)rm -rf
mkdir:= $(quiet)mkdir -p
echo := @echo
find := $(quiet)find
pcb2gcode := $(quiet)pcb2gcode $(if $V,,1>/dev/null)

# pcb2gcode configuations to generate
outdir := cnc
configs := \
	mill


# targets
all: strip-comments

.PHONY: strip-comments
strip-comments: $(patsubst %,$(outdir)/%,$(configs))
	$(find) $(outdir) -name '*.cnc' -exec sed -i 's:(.*)::' {} \;

clean:
	$(rm) $(outdir)
	$(rm) *#*

$(outdir)/%: %.pcb2gcode
	$(echo) generate cnc files with $<
	$(mkdir) $(outdir)
	$(pcb2gcode) --config $<
	$(rm) $(outdir)/*.svg
