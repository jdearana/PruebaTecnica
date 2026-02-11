
```typescript
import { describe, test, expect } from '@jest/globals';
import { getCapitalizeFirstWord } from './getCapitalizeFirstWord';

describe('getCapitalizeFirstWord', () => {
  test('throws an error when name is null', () => {
    expect(() => getCapitalizeFirstWord(null as unknown as string))
      .toThrow('Failed to capitalize first word with null');
  });

  test('returns empty string when name is empty', () => {
    expect(getCapitalizeFirstWord('')).toBe('');
  });

  test('capitalizes a single lowercase word', () => {
    expect(getCapitalizeFirstWord('hello')).toBe('Hello');
  });

  test('capitalizes a single uppercase word', () => {
    expect(getCapitalizeFirstWord('HELLO')).toBe('Hello');
  });

  test('capitalizes a single mixed case word', () => {
    expect(getCapitalizeFirstWord('HeLLo')).toBe('Hello');
  });

  test('does not modify single-letter word', () => {
    expect(getCapitalizeFirstWord('a')).toBe('a');
  });

  test('does not modify multiple single-letter words', () => {
    expect(getCapitalizeFirstWord('a b c')).toBe('a b c');
  });

  test('capitalizes multiple words correctly', () => {
    expect(getCapitalizeFirstWord('hello world')).toBe('Hello World');
  });

  test('handles mixed casing in multiple words', () => {
    expect(getCapitalizeFirstWord('jOhN dOE')).toBe('John Doe');
  });

  test('handles multiple words with single chars', () => {
    expect(getCapitalizeFirstWord('a b c hello')).toBe('a b c Hello');
  });

  test('preserves already title case', () => {
    expect(getCapitalizeFirstWord('Hello World')).toBe('Hello World');
  });

  test('handles extra spaces between words', () => {
    expect(getCapitalizeFirstWord('john  doe')).toBe('John  Doe');
  });
});
```