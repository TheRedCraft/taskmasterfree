# Migration from Claude API to DeepSeek R1 via OpenRouter

This document summarizes the changes made to migrate Task Master from using Claude API as the default provider to using DeepSeek R1 via OpenRouter's free tier.

## Changes Made

### 1. Core Configuration Updates

- **Default Provider Changed**: Updated `scripts/modules/config-manager.js` to use `openrouter` as the default provider instead of `anthropic`
- **Default Model Changed**: Updated default model from `claude-3-7-sonnet-20250219` to `deepseek/deepseek-r1-0528:free`
- **All Roles Updated**: Main, research, and fallback models all now use DeepSeek R1 by default
- **Token Limits Updated**: Increased default max tokens from various limits to 163,840 to match DeepSeek R1's capacity

### 2. Supported Models

- **Added DeepSeek R1**: Added `deepseek/deepseek-r1-0528:free` to `scripts/modules/supported-models.json`
- **Free Model**: Configured with 0 cost for both input and output tokens
- **All Roles Supported**: Can be used for main, research, and fallback roles
- **Friendly Name**: Added display name "DeepSeek R1 (Free)" for better UX

### 3. Documentation Updates

Updated the following files to reflect the new default provider:

- `README.md`: Updated main description and requirements section
- `assets/.windsurfrules`: Updated environment variable references
- `.taskmaster/docs/prd.txt`: Updated API configuration section
- `.taskmaster/docs/README.md`: Updated model references
- `CHANGELOG.md`: Added entry about the provider change
- `tests/e2e/run_e2e.sh`: Updated test default model

### 4. Environment Configuration

- **API Key Priority**: Moved `OPENROUTER_API_KEY` to the top of all configuration examples
- **Updated Examples**: Modified `assets/env.example` and `.cursor/mcp.json` to prioritize OpenRouter
- **Free Tier**: OpenRouter provides free access to DeepSeek R1, making it cost-effective

### 5. Example Configurations

Updated these configuration files to use the new defaults:
- `.taskmaster/config.json`
- `assets/config.json`

### 6. Test Updates

- Updated test files to expect the new default provider and model
- Fixed model ID references in configuration tests

## Benefits of the Migration

1. **Cost-Effective**: DeepSeek R1 is available for free via OpenRouter
2. **Large Context Window**: 163,840 tokens support larger projects
3. **High Performance**: DeepSeek R1 offers competitive performance
4. **Easy Migration**: Existing functionality remains intact
5. **Fallback Options**: Users can still configure Claude or other providers if needed

## Next Steps for Users

1. **Get OpenRouter API Key**: Sign up at https://openrouter.ai/ for a free API key
2. **Set Environment Variable**: Add `OPENROUTER_API_KEY` to your `.env` file or `.cursor/mcp.json`
3. **Existing Projects**: Will automatically use new defaults on next run
4. **Manual Override**: Use `task-master models --set-main <model>` to change if needed

## Backward Compatibility

- All existing functionality remains unchanged
- Users can still configure Claude or any other supported provider
- Existing configuration files are automatically migrated
- No breaking changes to the API or CLI commands

## Testing

The migration has been tested to ensure:
- Configuration loads correctly with new defaults
- DeepSeek R1 model is properly recognized
- All model roles (main, research, fallback) work correctly
- OpenRouter provider integration functions as expected

All features should continue to work as intended with the new default provider. 