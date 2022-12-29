# Applying the Microservice Architecture Pattern Language #
1. Value of pattern language exceeds sum of it's individual patterns (there are relationships between patterns)
	1. Predecessor: It is a pattern that motivates the need for this pattern
		1. Example: Microservices Architecture pattern is predecessor to rest of the patterns in pattern language (except monolithic architecture pattern)
	2. Successor: A pattern that **solves an issue introduced by this pattern**
		1. Example: If we apply Microservices Architecture pattern, we must apply numerous successor patterns (including service discovery patterns & circuit breaker pattern)
	3. Alternative: A pattern that provides an alternative solution to this pattern
		1. Example: Monolithic Architecture pattern & Microservices Architecture pattern are alternative ways to architect an application
			1. **Pick one or the other**
2. Recipe:
	1. **Applying a pattern causes issues that must then be addressed by applying successor patterns**
	2. **Select patterns continously recursively until we reach patterns with no successor**
	3. **If there are alternatives, pick one** (usually)
3. Following shows how to apply architecture pattern langauge to architect the application
	1. Three critical decisions are involved

## Decision #1: Monolithic Architecture or Microservice Architecture? ##
1. Choose between monolithic & microservices architecture
	1. If we choose microservices architecture pattern, we must choose other patterns as a consequence of the decision
		1. Successor patterns to apply:
			1. Deployment:
				1. Multiple services per host OR Single service per host
			3. Cross-cutting concern
				1. Microservice Chassis
				2. Externalized configuration
			4. Testing:
				1. Service Integration Contract Test
				2. Service Component Test
			5. Observability:
				1. Health Check API
				2. Application Metrics
				3. Audit Logging
				4. Application Logging
				5. Exception Tracking
				6. Distributed Tracing
			6. Decomposition:
				1. Decompose by business capability OR Decompose by subdomain
			7. UI:
				1. Server-side page fragment composition
				2. Client-side UI composition
			8. Security:
				1. Access Token
			9. Circuit Breaker
			10. Discovery:
				1. Service-side discovery OR Client-side discovery
			11. Style:
				1. Messaging OR Remote Procedure Invocation
			12. Communication:
				1. API Gateway
			13. Core:
				1. OR Monolithic Architecture
			14. Data:
				1. Database per Service

## Decision #2: How to Decompose an Application into Services? ##
1. Two main options to define services:
	1. Decompose by business capability: Define services corresponding to business capabilities
	2. Decompose by subdomain: Define services corresponding to DDD subdomains
2. The patterns yield equivalent results:
	1. **They are set of services organized around business concepts rather than technical concepts**

## Decision #3: How to Maintain Data Consistency and Perfom Queries? ##
1. Key feature of Microservice:
	1. Database per Service pattern
		1. It defines how we maintain data consistency and perform queries
			1. We might need to use **Saga pattern**
			2. We might need to implement queries using **Command Query Responsibility Segregation (CQRS)** pattern
	2. Alternative: Shared Database Pattern - It is an anti-pattern (best avoided)