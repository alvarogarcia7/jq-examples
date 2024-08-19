test: filter_then_select
	diff -q filter.actual.json filter.expected.json
	diff -q select.actual.json select.expected.json
	@echo "OK - All tests passing"
.PHONY: test

filter_then_select:
	jq '.[] | select(.parent_id == 10)' data.json > filter.actual.json
	jq '.[] | select(.parent_id == 10) | .id' data.json > select.actual.json
.PHONY: filter_then_select

