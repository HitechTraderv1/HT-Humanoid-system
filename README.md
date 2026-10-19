# Trading Robot

A research-first trading system designed to analyze markets consistently, follow explicit rules, protect capital, and improve only when evidence supports a change.

## Philosophy

Markets are uncertain. Studying price behavior, market structure, liquidity, volatility, and fundamentals can help form and test hypotheses, but no method can reliably predict every move or guarantee profit. The goal is not to make the bot "get richer and richer" at any cost; it is to make disciplined, measurable decisions while limiting the risk of ruin.

Automation can reduce human errors such as forgetting a rule or acting impulsively. It cannot remove risk: software bugs, bad data, changing market conditions, execution failures, and flawed assumptions can all cause losses. The system must be observable, tested, and able to stop safely.

## Operating principles

- **Protect capital first.** Every strategy needs defined risk limits, position sizing, stop conditions, and an emergency stop before it can place orders.
- **No setup, no trade.** The bot must be allowed to wait. A low-confidence or invalid setup is a reason to stand aside, not a reason to force a trade.
- **Evidence before deployment.** Separate research, backtesting, paper trading, and live trading. Include fees, spread, slippage, latency, and realistic order fills in evaluation.
- **Rules before machine learning.** Start with explainable rules and verified data. Learning components may propose changes, but must not silently rewrite safeguards or deploy themselves.
- **Measure uncertainty.** Confidence is not certainty. Track sample size, drawdown, out-of-sample performance, and the conditions under which a strategy fails.
- **Keep a record.** Save inputs, decisions, orders, risk checks, outcomes, and review notes so behavior can be audited and reproduced.

## Intended decision loop

```text
MARKET DATA
    ↓
MARKET CONDITION
    ↓
MARKET STRUCTURE
    ↓
SETUP DETECTION
    ↓
CONFLUENCE ANALYSIS
    ↓
TRADE VALIDATION
    ↓
RISK CALCULATION
    ↓
ENTRY DECISION (including NO TRADE)
    ↓
TRADE MANAGEMENT
    ↓
EXIT
    ↓
TRADE REVIEW
    ↓
LEARNING AND VALIDATED STRATEGY IMPROVEMENT
```

Each stage should have documented inputs, outputs, and failure behavior. Risk checks are a hard gate: a signal cannot override an account limit, invalid market data, or an emergency stop.

## Why traders fail—and what the bot must guard against

The failure library will cover overtrading, revenge trading, FOMO, entering without confirmation, excessive leverage, oversized positions, moving or removing stop losses irrationally, averaging into losing positions, trading unsuitable conditions, ignoring spread, slippage or news, strategy switching, curve fitting, over-optimization, trading without a setup, ignoring drawdown, poor risk/reward, emotional decisions, inconsistent execution, missing journals, and insufficient backtesting.

These are failure modes to detect and prevent, not a checklist that guarantees success. The bot should record which rules blocked an action and why it stood aside.

## Repository map

- `docs/` — learning and operating material, from foundations through professional workflow.
- `knowledge/` — reusable concepts, strategies, setups, patterns, indicators, market conditions, mistakes, and examples.
- `brain/` — analysis, setup detection, decisions, confidence, risk, position management, and learning components.
- `data/` — historical, live, processed, and trade data. Do not commit credentials or private account data.
- `backtesting/` — backtest engine, strategies, reports, and results.
- `execution/` — broker integration, orders, positions, and execution safeguards.
- `risk/` — account protection, daily limits, drawdown controls, and emergency stop.
- `learning/` — trade reviews, mistake analysis, performance tracking, and model versions.
- `tests/` — unit, strategy, risk, and execution tests.
- `config/` — trading, risk, and market configuration.

## Development stages

1. Document concepts and convert each strategy into precise, testable rules.
2. Validate market data and build reproducible research and backtesting.
3. Test against unseen periods and varied market conditions; account for costs and realistic fills.
4. Run in paper mode and verify order handling, logging, limits, and shutdown behavior.
5. Consider live execution only after review, with conservative limits and human oversight.
6. Review results and propose improvements; validate every change before adoption.

This project is educational and experimental software, not financial advice or a promise of returns. Live trading can lose some or all of the capital at risk. Do not connect a real account until the system has been independently reviewed and thoroughly tested.
