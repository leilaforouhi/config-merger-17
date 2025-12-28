#!/usr/bin/env python
"""
Config Merger
- Merges multiple JSON config files
- Later files override earlier ones
- Saves result into merged_config.json
"""

import json, sys

def main():
    if len(sys.argv) < 2:
        print("Usage: python3 merge_configs.py <config1.json> <config2.json> ...")
        sys.exit(1)

    merged = {}
    for path in sys.argv[1:]:
        try:
            with open(path, "r", encoding="utf-8") as f:
                data = json.load(f)
                merged.update(data)
        except Exception as e:
            print(f"Skipping {path}: {e}")

    with open("merged_config.json", "w", encoding="utf-8") as f:
        json.dump(merged, f, indent=2)

    print("Merged configuration saved to merged_config.json")

if __name__ == "__main__":
    main()
