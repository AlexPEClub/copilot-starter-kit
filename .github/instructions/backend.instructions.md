---
description: "Use when working on API routes, Supabase client, or database schemas. Covers RLS, input validation, query patterns, and security."
applyTo: "src/app/api/**,src/lib/supabase*,supabase/**"
---

# Backend Development Rules

## Database (Supabase)
- ALWAYS enable Row Level Security on every table
- Create RLS policies for SELECT, INSERT, UPDATE, DELETE
- Add indexes on columns used in WHERE, ORDER BY, and JOIN clauses
- Use foreign keys with ON DELETE CASCADE where appropriate
- Never skip RLS - security first

## API Routes
- Validate all inputs using Zod schemas before processing
- Always check authentication: verify user session exists
- Return meaningful error messages with appropriate HTTP status codes
- Use `.limit()` on all list queries

## Query Patterns
- Use Supabase joins instead of N+1 query loops
- Use `unstable_cache` from Next.js for rarely-changing data
- Always handle errors from Supabase responses

## Security
- Never hardcode secrets in source code
- Use environment variables for all credentials
- Validate and sanitize all user input
- Use parameterized queries (Supabase handles this)
