### Tips
- You don't need to know everything. Be honest about things you don't know
- Think it as a brainstorm session, it is your thought process that matters
- There is no one single answer, discuss different approaches and prons & cons
- The magic ingredient is honesty — you should always be confident in saying, "While I've never used technology X, I know it's a common solution to problem Y." 
- The combination of honesty, confidence, and a willingness to learn will leave a much better impression on your interviewer than throwing around incoherent tidbits about a product you’ve never really used in production.

### Step by Step Approach
While system design interviews are different, there are some common approaches to this.

1. Understand the goals
   1. Start with aligning the assumptions
      1. What is the goal of the system
      2. What are the constraints
      3. What are the inputs & outputs
      4. .....

2. Establish the scope
   1. Narrow down the feature sets to discuss with the interview
      1. Do we want to discuss end to end or just the API
      2. What clients to support
      3. Authentications?

3. Design for the Right Scale
   1. User Volume
   2. QPS
   3. Data Size
   4. Concurrency?
   5. Limitations?

4. Start High-Level, then Drill-Down
   1. Start by describing the end-to-end process based on the goals established
      1. Including detailing different clients, APIs, backend services, data stores, etc
   2. This will allow the conversation to drill down into potential performance bottlenecks, and decisions about the separation of responsibilities.
   3. Whichever approach you choose to start with, remember to always start simple, and iterate.

5. Data Stuctures and Algorithms
   1. Able to discuss complexity of something, such as hashing for `urlshortener`

6. Tradeoffs
   1. Show you understand the compromises and demonstrate knowledge regarding the pros and cons of different appraoches
   2. Examples like:
      - What type of database would you use and why?
      - What caching solutions are out there? Which would you choose and why?
      - What frameworks can we use as infrastructure in your ecosystem of choice?

7. [CheatSheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f)