# llm-deepseek

[![Changelog](https://img.shields.io/github/v/release/microdog/llm-deepseek?include_prereleases&label=changelog)](https://github.com/microdog/llm-deepseek/releases)
[![Tests](https://github.com/microdog/llm-deepseek/actions/workflows/test.yml/badge.svg)](https://github.com/microdog/llm-deepseek/actions/workflows/test.yml)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/microdog/llm-deepseek/blob/main/LICENSE)

DeepSeek V4.1 Flash and V4 Pro for the [LLM](https://llm.datasette.io/) CLI, with tool calling.

```bash
llm -m deepseek-v4-pro 'write a haiku about databases' \
  -o thinking enabled \
  -o reasoning_effort high
```

This is a fork of the original [rumisle/llm-deepseek](https://github.com/rumisle/llm-deepseek), maintained by [@microdog](https://github.com/microdog). The current tree inherits work from [dannyob/llm-deepseek](https://github.com/dannyob/llm-deepseek), which is itself a fork of the original. Both repositories have stopped accepting pull requests.

The inherited work includes two contributions that were never merged upstream:

- DeepSeek v4 models (`deepseek-v4-flash`, `deepseek-v4-pro`) plus the `thinking` and `reasoning_effort` options, by [@microdog](https://github.com/microdog) ([PR](https://github.com/rumisle/llm-deepseek/pull/5))
- Tool calling for all DeepSeek models, by [@michaelmdeng](https://github.com/michaelmdeng) ([PR](https://github.com/rumisle/llm-deepseek/pull/3))

## Install

Not published to PyPI — install directly from git:

```bash
llm install git+https://github.com/microdog/llm-deepseek.git
```

## Usage

Obtain a [DeepSeek API key](https://platform.deepseek.com/api_keys) and save it:

```bash
llm keys set deepseek
# <Paste key here>
```

Run `llm models` to see registered models. Then:

```bash
llm -m deepseek-flash 'five great names for a pet ocelot'
llm -m deepseek-v4-pro 'solve \int \frac{\ln(x)\arctan(x)}{x^2+1} dx'
llm -m deepseek-flash 'how to reverse a linked list in python'
llm -m deepseek-v4-pro 'explain how vector databases work'
```

`deepseek-flash` is the current V4.1 Flash model (1M context, text and image
input). `deepseek-v4-pro` is the V4 Pro model. The legacy names
`deepseek-v4-flash` and `deepseek-v4-flash-vision-exp` are also registered for
compatibility; the API routes them to V4.1 Flash. The discontinued
`deepseek-chat`, `deepseek-reasoner`, and `deepseek-coder` names are not
registered.

Standard OpenAI-compatible options work (`max_tokens`, `top_p`, `stop`, `json_object`), plus DeepSeek-specific ones (`thinking`, `reasoning_effort`).

## Development

```bash
cd llm-deepseek
python3 -m venv venv
source venv/bin/activate
llm install -e '.[test]'
pytest
```
