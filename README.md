# web-components

Collection of web components I use across projects.

## How to use the components in other projects?

- Simplest: copy the code from this repo.
- Advanced: Add this script to a Makefile to easily udpate the components to the lastest versions when needed:

```Makefile
COMPONENTS := horizontal-carousel install-button share-url
REPO_URL := https://github.com/tomyo/web-components.git
COMPONENTS_DIR := components
BRANCH := main
# DEST_DIR is the local project directory where the components live
DEST_DIR := components

update-components:
	@echo "🌀 Fetching components from $(REPO_URL)"
	$(eval TEMP_DIR := $(shell mktemp -d))
	git clone $(REPO_URL) $(TEMP_DIR)
	cd $(TEMP_DIR) && git checkout $(BRANCH)
	cd $(COMPONENTS_DIR)

	@echo "🔄 Syncing files..."
	mkdir -p $(DEST_DIR)
	for c in $(COMPONENTS); do \
			echo "→ $$c"; \
			rm -rf $(DEST_DIR)/$$c/*; \
			mkdir -p $(DEST_DIR)/$$c; \
			cp -r $(TEMP_DIR)/$(COMPONENTS_DIR)/$$c/* $(DEST_DIR)/$$c/; \
	done

	@echo "🧹 Cleaning up..."
	rm -rf $(TEMP_DIR)

	@echo "✅ Components updated successfully!"
```
