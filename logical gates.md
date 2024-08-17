### 1. **AND Gate**
- **Symbol:** `A ∧ B`
- **Truth Table:**
  | A | B | A ∧ B |
  |---|---|-------|
  | 0 | 0 |   0   |
  | 0 | 1 |   0   |
  | 1 | 0 |   0   |
  | 1 | 1 |   1   |

- **Properties:**
  - Output is `1` only when all inputs are `1`.
  - Commutative: `A ∧ B = B ∧ A`
  - Associative: `(A ∧ B) ∧ C = A ∧ (B ∧ C)`
  - Identity: `A ∧ 1 = A`
  - Null Element: `A ∧ 0 = 0`
  - Idempotent: `A ∧ A = A`
  - Absorption: `A ∧ (A ∨ B) = A`
  - Distributive: `A ∧ (B ∨ C) = (A ∧ B) ∨ (A ∧ C)`

### 2. **OR Gate**
- **Symbol:** `A ∨ B`
- **Truth Table:**
  | A | B | A ∨ B |
  |---|---|-------|
  | 0 | 0 |   0   |
  | 0 | 1 |   1   |
  | 1 | 0 |   1   |
  | 1 | 1 |   1   |

- **Properties:**
  - Output is `1` if at least one input is `1`.
  - Commutative: `A ∨ B = B ∨ A`
  - Associative: `(A ∨ B) ∨ C = A ∨ (B ∨ C)`
  - Identity: `A ∨ 0 = A`
  - Null Element: `A ∨ 1 = 1`
  - Idempotent: `A ∨ A = A`
  - Absorption: `A ∨ (A ∧ B) = A`
  - Distributive: `A ∨ (B ∧ C) = (A ∨ B) ∧ (A ∨ C)`

### 3. **NOT Gate**
- **Symbol:** `¬A` or `A'`
- **Truth Table:**
  | A | ¬A |
  |---|----|
  | 0 |  1 |
  | 1 |  0 |

- **Properties:**
  - Inverts the input: `1` becomes `0`, and `0` becomes `1`.
  - Involution: `¬(¬A) = A`
  - Complement: `A ∧ ¬A = 0`, `A ∨ ¬A = 1`
  
### 4. **NAND Gate**
- **Symbol:** `A ↑ B` or `A | B`
- **Truth Table:**
  | A | B | A ↑ B |
  |---|---|-------|
  | 0 | 0 |   1   |
  | 0 | 1 |   1   |
  | 1 | 0 |   1   |
  | 1 | 1 |   0   |

- **Properties:**
  - Inverse of AND gate: Output is `1` unless all inputs are `1`.
  - Noncommutative: Not an associative operation.
  - Used in constructing any other logical gate (NAND is functionally complete).

### 5. **NOR Gate**
- **Symbol:** `A ↓ B`
- **Truth Table:**
  | A | B | A ↓ B |
  |---|---|-------|
  | 0 | 0 |   1   |
  | 0 | 1 |   0   |
  | 1 | 0 |   0   |
  | 1 | 1 |   0   |

- **Properties:**
  - Inverse of OR gate: Output is `1` only when all inputs are `0`.
  - Noncommutative: Not an associative operation.
  - Functionally complete (like NAND, can construct any other logical gate).

### 6. **XOR (Exclusive OR) Gate**
- **Symbol:** `A ⊕ B`
- **Truth Table:**
  | A | B | A ⊕ B |
  |---|---|-------|
  | 0 | 0 |   0   |
  | 0 | 1 |   1   |
  | 1 | 0 |   1   |
  | 1 | 1 |   0   |

- **Properties:**
  - Output is `1` if and only if the inputs are different.
  - Commutative: `A ⊕ B = B ⊕ A`
  - Associative: `(A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)`
  - Identity: `A ⊕ 0 = A`
  - Inverse: `A ⊕ A = 0`
  - Distributive: `A ⊕ (B ∧ C) = (A ⊕ B) ∧ (A ⊕ C)`

### 7. **XNOR (Exclusive NOR) Gate**
- **Symbol:** `A ⊙ B`
- **Truth Table:**
  | A | B | A ⊙ B |
  |---|---|-------|
  | 0 | 0 |   1   |
  | 0 | 1 |   0   |
  | 1 | 0 |   0   |
  | 1 | 1 |   1   |

- **Properties:**
  - Output is `1` if the inputs are the same.
  - Commutative: `A ⊙ B = B ⊙ A`
  - Associative: `(A ⊙ B) ⊙ C = A ⊙ (B ⊙ C)`
  - Identity: `A ⊙ 1 = ¬A`
  - Inverse: `A ⊙ A = 1`
  - Distributive: `A ⊙ (B ∧ C) = (A ⊙ B) ∧ (A ⊙ C)`
