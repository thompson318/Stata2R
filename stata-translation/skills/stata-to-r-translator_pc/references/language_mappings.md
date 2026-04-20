# Stata → R Language Mappings
## artbin package (v2.1.2)

Catalogued from `artbin.ado`, `art2bin.ado`, and `artformatnos.ado`.

---

## 1. Statistical / Mathematical Functions

| Stata | R | Notes |
|---|---|---|
| `invnormal(p)` | `qnorm(p)` | |
| `invnorm(p)` | `qnorm(p)` | Alias used in artbin.ado |
| `normal(x)` | `pnorm(x)` | |
| `normprob(x)` | `pnorm(x)` | Alias used in artbin.ado |
| `invchi2(df, p)` | `qchisq(p, df)` | **Argument order swapped** |
| `nchi2(df, ncp, x)` | `pchisq(x, df, ncp)` | **Argument order swapped** |
| `npnchi2(df, x, p)` | custom `.npnchi2(df, x, p)` | No direct equivalent; use `uniroot` to invert `pchisq` |
| `ceil(x)` | `ceiling(x)` | |
| `floor(x)` | `floor(x)` | Same name |
| `round(x, unit)` | `round(x / unit) * unit` | Stata rounds to nearest `unit`; R `round(x, digits)` rounds to decimal places |
| `abs(x)` | `abs(x)` | Same |
| `sqrt(x)` | `sqrt(x)` | Same |
| `sign(x)` | `sign(x)` | Same |
| `log(x)` | `log(x)` | Both natural log |
| `exp(x)` | `exp(x)` | Same |
| `max(a, b)` | `max(a, b)` | Same for scalars; `pmax()` for vectors |
| `min(a, b)` | `min(a, b)` | Same for scalars; `pmin()` for vectors |
| `acos(x)` | `acos(x)` | Same |
| `cos(x)` | `cos(x)` | Same |
| `_pi` | `pi` | Built-in constant |
| `cond(test, a, b)` | `ifelse(test, a, b)` | |
| `mi(x)` (missing string macro) | `is.null(x)` or `nchar(x) == 0` | Context-dependent: `is.null` for absent args, `is.na` for numeric NA |

---

## 2. Program Structure

| Stata | R | Notes |
|---|---|---|
| `program define foo, rclass` | `foo <- function(...) { ... }` | R functions return values via `return()` or last expression |
| `syntax , OPT(type) [OPT2]` | function arguments with defaults | Required args have no default; optional args have `= NULL` or typed default |
| `return scalar x = val` | `list(x = val)` in return value | Collect all results into a named list |
| `return local x = "str"` | include as `x = "str"` in return list | |
| `` r(x) `` | `result$x` | Accessing named element of returned list |
| `di as err "msg"; exit 198` | `stop("msg")` | |
| `di as text "msg"` (warning/note) | `warning("msg")` or `message("msg")` | `message()` for informational; `warning()` for recoverable issues |
| `cap prog drop foo` | not needed | R functions are simply reassigned |
| `version 8` | not needed | No Stata version compatibility needed |
| `_caller() >= 12` | not needed | |

---

## 3. Macros and Variable Assignment

| Stata | R | Notes |
|---|---|---|
| `local x = val` | `x <- val` | Numeric assignment |
| `local x str` | `x <- "str"` | String assignment (no quotes needed in Stata) |
| `` `x' `` | `x` | Macro expansion → plain variable reference |
| `local ++x` | `x <- x + 1` | |
| `local x`y'`` (concatenation) | `paste0(x, y)` | |
| `$global_macro` | function argument or env var | Avoid globals; pass as argument |
| `$S_level` | fixed as `95` or passed as arg | Stata's global confidence level setting |

---

## 4. String Tokenisation and Parsing

| Stata | R | Notes |
|---|---|---|
| `tokenize "str"` then `` `1', `2', ... `` | `parts <- strsplit(str, " ")[[1]]`; `parts[1]`, `parts[2]` | |
| `macro shift` | (iterate `parts` with index) | Replace while-loop-with-macro-shift with `for (tok in parts)` |
| `gettoken x rest : str, parse(" ,")` | `x <- strsplit(str, "[ ,]+")[[1]][1]` | |
| `numlist "str"` | `as.numeric(strsplit(str, " ")[[1]])` | |
| `word count str` | `length(strsplit(trimws(str), "\\s+")[[1]])` | |
| `` `word N of str' `` | `strsplit(str, " ")[[1]][N]` | |
| `` "`x'"=="" `` | `is.null(x) \|\| x == ""` | |
| `` !mi("`x'") `` | `!is.null(x) && nchar(x) > 0` | |
| `confirm number x` | `if (!is.numeric(x)) stop(...)` | |
| `parse "str", parse("sep")` | `strsplit(str, sep)` | |

---

## 5. Control Flow

| Stata | R | Notes |
|---|---|---|
| `forvalues i=1/n { ... }` | `for (i in 1:n) { ... }` | |
| `foreach x in list { ... }` | `for (x in list) { ... }` | |
| `while cond { ... }` | `while (cond) { ... }` | |
| `if cond { ... } else { ... }` | `if (cond) { ... } else { ... }` | Same structure |
| `if _rc { ... }` (after `cap`) | `tryCatch(...)` | Stata's `cap` suppresses errors; use `tryCatch` in R |
| `cap assert cond; if _rc { stop }` | `if (!cond) stop(...)` | |
| `local i 0; while ... { local i=\`i'+1 }` | `i <- 0; while (...) { i <- i + 1 }` | Standard counter loop |

---

## 6. In-Memory Dataset Operations (k-group section)

The k-group code uses a temporary Stata dataset to hold per-group vectors.
These translate to plain R vectors — no dataset needed.

| Stata | R | Notes |
|---|---|---|
| `preserve` / `restore` | not needed | R has no global dataset to protect |
| `drop _all` | not needed | |
| `set obs n` | (allocate vectors of length n) | `PI <- rep(NA_real_, n)` |
| `gen double x = .` | `x <- rep(NA_real_, n)` | |
| `replace x = val in i` | `x[i] <- val` | |
| `summ x [w=w], meanonly` | `weighted.mean(x, w)` | |
| `summ x, meanonly` → `r(mean)`, `r(max)`, `r(min)` | `mean(x)`, `max(x)`, `min(x)` | |
| `gen double y = f(x)` | `y <- f(x)` | Vectorised in R |
| `replace y = f(x)` | `y <- f(x)` | |
| `_n` (observation number) | `seq_along(x)` or `1:n` | |
| `_N` (total observations) | `length(x)` or `n` | |
| `x[i]` (scalar subscript in Stata) | `x[i]` | Same syntax |

---

## 7. Matrix Operations (k-group Wald test)

| Stata | R | Notes |
|---|---|---|
| `mat M = J(K, K, 0)` | `M <- matrix(0, K, K)` | |
| `mat M[k, l] = val` | `M[k, l] <- val` | Same syntax |
| `mkmat x if _n>1` | `as.matrix(x[-1])` | Drops first element (reference group) |
| `mat Q = v' * syminv(M) * v` | `Q <- t(v) %*% solve(M) %*% v` | `syminv` = inverse of symmetric matrix = `solve` |
| `M[1,1]` (scalar from matrix) | `M[1,1]` | Same syntax |

---

## 8. Output and Formatting

| Stata | R | Notes |
|---|---|---|
| `di as text "label" _col(N) as res val` | `cat(sprintf("%-Ns%s\n", label, val))` or formatted message | artbin uses `_col(40)` throughout |
| `di as text "{hline N}"` | `cat(strrep("-", N), "\n")` | |
| `display format val` (e.g. `%5.3f`) | `formatC(val, format="f", digits=3)` or `sprintf("%.3f", val)` | |
| `%5.3f` format | `sprintf("%5.3f", x)` | |
| `%-6.3f` format (left-justified) | `formatC(x, format="f", digits=3, flag="-")` | |
| `%-9.2f` format | `formatC(x, format="f", digits=2, width=9, flag="-")` | |
| `length("str")` | `nchar("str")` | |
| `artformatnos` (line-wrapping utility) | Custom R function (see `artformatnos.md`) | |
| `frac_ddp x n` | `round(x, n)` | Stata utility for display rounding |

---

## 9. Internal Subroutines → R Functions

| Stata subroutine | R equivalent | Location |
|---|---|---|
| `_inrange01 x1 x2 ...` | `all(c(x1, x2, ...) > 0 & c(x1, x2, ...) < 1)` | Inline; or helper `.inrange01()` |
| `_cc, n() ad() [r() deflate()]` | `.cc(n, adiff, ratio=1, deflate=FALSE)` | `R/art2bin.R` |
| `_sp varlist [, out()]` | `sum(v1 * v2 * ...)` | Inline; or `.sp()` helper |
| `_pe2 a0 q0 a1 q1 k n a b` | `.pe2(a0, q0, a1, q1, k, n, a)` returning beta | `R/kgroup.R` |
| `frac_ddp x n` | `round(x, n)` | Inline |
| `artformatnos` | `.artformatnos(n, maxlen, ...)` | `R/utils.R` (if output table needed) |

---

## 10. Custom R Implementation Required

These Stata functions have no direct R equivalent and need bespoke implementations:

| Stata | R implementation needed | Reason |
|---|---|---|
| `npnchi2(df, x, p)` | `.npnchi2 <- function(df, x, p) uniroot(function(ncp) pchisq(x, df, ncp) - p, ...)$root` | Inverts noncentral chi2 CDF; no base R equivalent |
| `_pi` constant in `acos` context | `pi` | Trivial but note Stata's `_pi` vs R's `pi` |
| `invchi2(df, p)` arg order | `qchisq(p, df)` | Arg order differs — common source of bugs |
| `nchi2(df, ncp, x)` arg order | `pchisq(x, df, ncp)` | Arg order differs — common source of bugs |
