**Building Applications with AI Agents** Designing and Implementing Multiagent Systems


### **CHAPTER 1 Introduction to Agents**

We are witnessing a profound technological transformation driven by autonomous agents—intelligent software systems capable of independent reasoning, decision making, and interacting effectively within dynamic environments. Unlike traditional software, autonomous agents interpret contexts, adapt to changing scenarios, and perform sophisticated actions with minimal human oversight.

###### **Defining AI Agents**

Autonomous agents are intelligent systems designed to independently analyze data, interpret their environment, and make context-driven decisions. As the popularity of the term “agent” grows, its meaning has become diluted, often applied to systems lacking genuine autonomy. In practice, agency exists on a spectrum. True autonomous agents demonstrate meaningful decision making, context-driven reasoning, and adaptive behaviors. Conversely, many systems labeled as “agents” may simply execute deterministic scripts or tightly controlled workflows. Designing genuinely autonomous, adaptive agents is challenging, prompting many teams to adopt simpler approaches to achieve quicker outcomes. Therefore, the key test of a true agent is whether it demonstrates real decision making rather than following static scripts.

The rapid evolution of autonomous agents is primarily driven by breakthroughs in foundation models and reinforcement learning. While traditional use cases with foundation models have focused on generating human-readable outputs, the latest advances enable these models to generate structured function signatures and parameter selections. Orchestration frameworks can then execute these functions—enabling agents to look up data, manipulate external systems, and perform concrete actions. Throughout this book, we will use the term “agentic system” to describe the full supporting functionality that enables an agent to run effectively, including the tools, memory, foundation model, orchestration, and supporting infrastructure.

With a growing range of protocols such as Model Context Protocol (discussed in Chapter 4) and Agent-to-Agent Protocol (discussed in Chapter 8), these agents will be able to use remote tools and collaborate with other agents to solve problems. This unlocks enormous opportunities for sophisticated automation—but it also brings a profound responsibility to design, measure, and manage these systems thoughtfully, ensuring their actions align with human values and operate safely in complex, dynamic environments.

###### **The Pretraining Revolution**

While traditional ML is an incredibly powerful technique, it is usually limited by the quantity and quality of the dataset. ML practitioners will typically tell you that they spend the majority of their time not training models, but on collecting and cleaning datasets that they can use for training. The incredible success of generative models that have been trained on large volumes of data have shown that single models can now adapt to a wide range of tasks without any additional training. This upends years of practice. To build an application that used ML previously required hiring an ML engineer or data scientist, having them collect data, and then deploying that model. With the latest developments in large, pretrained generative models, high-quality models that will work reasonably well for many use cases are now available through a single call to a hosted model without any training or hosting required. This dramatically lowers the cost and complexity of building applications enabled with ML and AI.

Recent advancements in large language models (LLMs) such as GPT-5, Anthropic’s Claude, Meta’s Llama, Google’s Gemini Ultra, and DeepSeek’s V3 have increased the performance on a range of difficult tasks even further, widening the scope of problems solvable with pretrained models. These foundation models offer robust natural language understanding and content generation capabilities, enhancing agent functionality through:

###### _Natural language understanding_

Interpreting and responding intuitively to user inputs

###### _Context-aware interaction_

Maintaining context for relevant and accurate responses over extended interactions

###### _Structured content generation_

Producing text, code, and structured outputs essential for analytical and creative tasks

While these models are very capable on their own, they can also be used to make decisions within well-scoped areas, adapt to new information, and invoke tools to accomplish real work. Integration with sophisticated orchestration frameworks

enables these models to interact directly with external systems and execute practical tasks. These models are capable of:

###### _Contextual interpretation and decision making_

Navigating ambiguous situations without exhaustive preprogramming

###### _Tool use_

Calling other software to retrieve information or take actions

###### _Adaptive planning_

Planning and executing complex, multistep actions autonomously

###### _Information summarization_

Rapidly processing extensive documents, extracting key insights, thereby aiding legal analysis, research synthesis, and content curation

###### _Management of unstructured data_

Interpreting and responding intelligently to unstructured texts such as emails, documents, logs, and reports

###### _Code generation_

Writing and executing code and writing unit tests

###### _Routine task automation_

Efficiently handling repetitive activities in customer service and administrative workflows, freeing human workers to focus on more nuanced tasks

###### _Multimodal information synthesis_

Performing intricate analyses of image, audio, or video data at scale

This enhanced flexibility enables autonomous agents to effectively handle complex and dynamic scenarios that static ML models typically cannot address.

###### **Types of Agents**

As the term “agent” has gained popularity, its meaning has broadened to encompass a wide range of AI-enabled systems, often creating confusion about what truly constitutes an AI agent. _The Information_ categorizes agents into seven practical types, reflecting how these technologies are being applied today:

###### _Business-task agents_

These agents automate predefined business workflows, such as UiPath’s robotic process automation, Microsoft Power Automate’s low-code flows, or Zapier’s app integrations. They execute sequences of deterministic actions, typically triggered by events, with minimal contextual reasoning.

###### _Conversational agents_

This category includes chatbots and customer service agents that engage users through natural language interfaces. They are optimized for dialogue management, intent recognition, and conversational turn-taking, such as virtual assistants embedded in customer support platforms.

###### _Research agents_

Research agents conduct information gathering, synthesis, and summarization tasks. They scan documents, knowledge bases, or the web to provide structured outputs that assist human analysts. Examples include Perplexity AI and Elicit.

###### _Analytics agents_

Analytics agents, such as Power BI Copilot or Glean, focus on interpreting structured datasets and generating insights, dashboards, and reports. They often integrate tightly with enterprise data warehouses, enabling users to query complex data in natural language.

###### _Developer agents_

Tools like Cursor, Windsurf, and GitHub Copilot represent coding agents, which assist developers by generating, refactoring, and explaining code. They integrate deeply into IDE workflows to augment software development productivity.

###### _Domain-specific agents_

These agents are tuned for specialized professional domains, such as legal (Harvey), medical (Hippocratic AI), or finance agents. They combine domain-specific knowledge with structured workflows to deliver targeted, expert-level assistance.

###### _Browser-using agents_

These agents navigate, interact with, extract information from, and take actions on websites without human interaction. As opposed to traditional robotic process automation, which follows prescripted steps, modern browser-using agents combine language understanding, visual perception, and dynamic planning to adapt on the fly.

In addition to these seven types of agents, voice and video agents are important and also expected to increase in adoption in the coming years:

###### _Voice agents_

Powered by end-to-end speech understanding and generation, these agents are enabling conversational automation in areas like customer service, appointment scheduling, and even real-time order processing.

###### _Video agents_

These agents present users with avatar-based video responses, combining lipsynced speech, facial expression, and gesture. They’re emerging rapidly in sales,

training, customer onboarding, marketing, and virtual presence tools—enabling scalable, personalized video interactions without manual production.

Importantly, the number and variety of agent types is growing rapidly, and we will likely see new kinds of agents emerge across many domains as the field and its underlying technologies evolve. In this book, our emphasis is on the core category of agents built around language models, particularly those using text and code. While we touch on business task automation, voice, and video, we’ll primarily explore agents built around language models—their architectures, reasoning, and UX—in subsequent chapters.

Now that we’ve discussed the evolving types of agents, the next critical question becomes: which model should you choose to power your agent? Model selection is a complex and rapidly changing domain. As discussed in the next section, you’ll need to balance factors like task complexity, modality support, latency and cost constraints, and integration requirements to make the right choice for your agent.

###### **Model Selection**

Today, we are fortunate to have a proliferation of powerful models available from both commercial providers and the open source community. OpenAI, Anthropic, Google, Meta, and DeepSeek each offer state-of-the-art foundation models with impressive general-purpose capabilities. At the same time, open-weight models like Llama, Mistral, and Gemma are pushing the boundaries of what can be achieved with local or fine-tuned deployments. Even more striking is the rapid advancement of small- and medium-sized models. New techniques for distillation, quantization, and synthetic data generation are enabling compact models to inherit surprising levels of capability from their larger counterparts.

This explosion of choice is good news: competition is driving faster innovation, better performance, and lower costs. But it also creates a dilemma—how do you choose the right model for your agentic system? The truth is, there isn’t a one-size-fits-all answer. In fact, one of the most reasonable starting points is simply to use the latest generalpurpose model from a leading provider like OpenAI or Anthropic. As you can see in Table 1-1, these models offer strong performance out of the box, require little customization, and will take you surprisingly far for many applications. GPT-5 mini (Aug 2025) leads overall with the highest mean score (0.819), closely followed by o4mini (0.812) and o3 (0.811). Proprietary and open-access models like Qwen3, Grok 4, Claude 4, and Kimi K2 also show competitive results.

_Table 1-1. HELM Core Scenario leaderboard (August 2025). Comparative benchmark performance of the top 10 models across reasoning and evaluation tasks: MMLU-Pro, GPQA, IFEval, WildBench, and Omni-MATH._

That said, they aren’t always the most efficient choice. For many tasks—especially those that are well-defined, low-latency, or cost-sensitive—much smaller models can provide near-equivalent performance at a fraction of the cost. This has led to a growing trend: automated model selection. Some platforms now route simpler queries to fast, inexpensive small models, reserving the large, expensive models for more complex reasoning. This dynamic test-time optimization is proving effective, and it hints at a future where multimodel systems become the norm.

The key takeaway is that you can spend enormous effort optimizing model selection for marginal gains—but unless your scale or constraints demand it, starting simple is fine. Over time, it’s often worth experimenting with smaller models, fine-tuning, or adding retrieval to improve performance and reduce costs. Just remember: the future is almost certainly multimodel, and designing for flexibility now will pay off later.

###### **From Synchronous to Asynchronous Operations**

Traditional software systems typically execute tasks synchronously, moving step-bystep and waiting for each action to finish before starting the next. While this approach is straightforward, it can lead to significant inefficiencies—especially when waiting on external inputs or processing large volumes of data.

In contrast, autonomous agents are designed for asynchronous operation. They can manage multiple tasks in parallel, swiftly adapt to new information, and prioritize

actions dynamically based on changing conditions. This asynchronous processing dramatically enhances efficiency, reducing idle time and optimizing the use of computational resources.

The practical implications of this shift are substantial. For example:

- Emails can arrive with reply drafts already prepared.

- Invoices can come with pre-populated payment details.

- Software engineers might receive tickets accompanied by code to solve them and unit tests to assess them.

- Customer support agents can be provided with suggested responses and recommended actions.

- Security analysts can receive alerts that have already been automatically investigated and enriched with relevant threat intelligence.

In each case, agents are not just speeding up routine workflows—they are changing the nature of work itself. This evolution transforms human roles from task executors to task managers. Rather than spending time on repetitive or mechanical steps, individuals can focus on strategic oversight, review, and high-value decision making— amplifying human creativity and judgment while letting agents handle the operational details. These agents make it much easier for human roles to be proactive rather than reactive.

###### **Practical Applications and Use Cases**

The versatility of autonomous agents opens up a myriad of applications across different industries. To keep this book grounded in clear, specific use cases, I have seven real-world example agents with evaluation systems available in the public GitHub repo supporting this book. We will frequently turn back to these examples as we explore the key aspects of agent systems:

###### _Customer support agent_

Customer support is one of the most prevalent applications for autonomous agents. These agents handle common inquiries, process refunds, update orders, and escalate complex issues to human representatives, providing 24/7 support while enhancing customer satisfaction and reducing operational costs.

###### _Financial services agent_

In banking and financial services, agents assist with account management, loan processing, fraud investigation, and investment portfolio rebalancing. They streamline customer service, accelerate transaction processing, and improve security by detecting suspicious activities in real time.

###### _Healthcare patient intake and triage agent_

These agents support frontline healthcare operations by registering new patients, verifying insurance, assessing symptoms to prioritize care, scheduling appointments, managing medical histories, and coordinating referrals, thereby improving workflow efficiency and patient outcomes.

###### _IT help desk agent_

IT help desk agents manage user access, troubleshoot network and system issues, deploy software updates, respond to security incidents, and escalate unresolved issues to specialists. They enhance productivity by resolving common technical problems swiftly.

###### _Legal document review agent_

Legal agents assist attorneys and paralegals by reviewing contracts, conducting legal research, performing client intake and conflict checks, managing discovery, assessing compliance, calculating damages, and tracking deadlines. This helps to streamline workflows and improve accuracy in legal operations.

###### _Security Operations Center (SOC) analyst agent_

SOC analyst agents investigate security alerts, gather threat intelligence, query logs, triage incidents, isolate compromised hosts, and provide updates to security teams. They accelerate incident response and strengthen organizational security posture.

###### _Supply chain and logistics agent_

In supply chain management, agents optimize inventory, track shipments, evaluate suppliers, coordinate warehouse operations, forecast demand, manage disruptions, and handle compliance requirements. These capabilities help maintain resilience and efficiency across global networks.

Autonomous agents offer significant potential across various use cases, from customer support and personal assistance to legal services and advertising. By integrating these agents into their operations, organizations can achieve greater efficiency, improve service quality, and unlock new opportunities for innovation and growth. As we continue to explore the capabilities and applications of autonomous agents in this book, it becomes evident that their impact will be profound and far-reaching across multiple industries.

Now that we’ve looked at some example agents, in the next section, we’ll discuss some of the key considerations when designing our agentic systems.

###### **Workflows and Agents**

In many real‐world projects, choosing between a simple script, a deterministic workflow, a traditional chatbot, a retrieval‐augmented generation (RAG) system, or a

full‐blown autonomous agent can be the difference between an elegant solution and an overengineered, hard‐to‐maintain mess. To make this choice clearer, consider four key factors: the variability of your inputs, the complexity of the reasoning required, any performance or compliance constraints, and the ongoing maintenance burden.

First, when might you choose not to use a foundation model—or any ML component at all? If your inputs are fully predictable and every possible output can be described in advance, a handful of lines of procedural code are often faster, cheaper, and far easier to test than an ML–based pipeline. For example, parsing a log file that always follows the format “YYYY‐MM‐DD HH:MM:SS—message” can be handled reliably with a small regular‐expression‐based parser in Python or Go. Likewise, if your application demands millisecond‐level latency—such as an embedded system that must react to sensor data in real time—there simply isn’t time for a language model API call. In such cases, traditional code is the right choice. Finally, regulated domains (medical devices, aeronautics, certain financial systems) often require fully deterministic, auditable decision logic—black‐box neural models won’t satisfy certification requirements. If any of these conditions hold—deterministic inputs, strict performance or explainability needs, or a static problem domain—plain code is almost always preferable to a foundation model.

Next, consider deterministic or semiautomated workflows. Here, the logic can be expressed as a finite set of steps or branches, and you know ahead of time where you might need human intervention or extra error handling. Suppose you ingest invoices from a small set of vendors and each invoice arrives in one of three known formats: CSV, JSON, or PDF. You can build a workflow that routes each format to its corresponding parser, checks for mismatches, and halts for a human review if any fields fail a simple reconciliation—no deep semantic understanding is required. Likewise, if your system must retry failed steps with exponential backoff or pause for a manager’s approval, a workflow engine (such as Airflow, AWS Step Functions, or a wellstructured set of scripts) offers clearer control over error paths than an LLM could. Deterministic workflows make sense whenever you can enumerate all decision branches in advance and you need tight, auditable control over each branch. In such scenarios, workflows scale more naturally than large, ad hoc scripts but still avoid the complexity and cost of running an agentic pipeline.

Traditional chatbots or RAG systems occupy the next tier of complexity: they add natural language understanding and document retrieval but stop short of autonomous, multistep planning. If your primary need is to let users ask questions about a knowledge base—say, searching a product manual, a legal archive, or corporate wikis —a RAG system can embed documents into a vector store, retrieve relevant passages in response to a query, and generate coherent, context‐aware answers. For instance, an internal IT help desk might use RAG to answer “How do I reset my VPN credentials?” by fetching the latest troubleshooting guide and summarizing the relevant steps. Unlike autonomous agents, RAG systems do not independently decide on

follow‐up actions (like filing a ticket or scheduling a callback); they simply surface information. A traditional chatbot or RAG approach makes sense when the task is primarily question‐answering over structured or unstructured content, with limited need for external API calls or decision orchestration. Maintenance costs are lower than for agents—your main overhead lies in keeping document embeddings up to date and refining prompts—but you sacrifice the agent’s ability to plan multistep workflows or learn from feedback loops.

Finally, we reach autonomous agents—situations where neither simple code, nor rigid workflows, nor RAG suffice because inputs are unstructured, novel, or highly variable, and because you require dynamic, multistep planning or continuous learning from feedback. Consider a customer support center that receives free‐form emails with issues ranging from “my laptop battery is swelling and might erupt” to “I keep getting billed for services I didn’t order.” A rule‐based workflow or a RAG‐powered FAQ lookup would shatter under such open‐ended variety, but an agent powered by a foundation model can parse intent, extract relevant entities, consult a knowledge base, draft an appropriate response, and even escalate to a human if necessary—all without being told every possible branch in advance. Similarly, in supply chain management, an agent that ingests real‐time inventory data, supplier lead times, and sales forecasts can replan shipment schedules dynamically; a deterministic workflow would require constant manual updates to handle new exceptions.

Agents also excel when many subtasks must run in parallel—such as a security operations agent that simultaneously queries threat intelligence APIs, scans network telemetry, and performs sandbox analysis on suspicious binaries. Because agents operate asynchronously and reprioritize based on real‐time data, they avoid the brittle “onestep‐at‐a‐time” nature of workflows or RAG systems. To justify the higher compute and maintenance costs of running a foundation model, you need this level of contextual reasoning, parallel task orchestration, or ongoing self‐improvement—scenarios where rigid code, workflows, or chatbots would be too brittle or expensive to maintain.

_Table 1-2. Distinguishing workflows and agents from traditional code_

Every path carries trade‐offs. Pure code is cheap and fast but inflexible; workflows offer control but break down when inputs grow wildly variable; traditional chatbots or RAG are great for question‐answering over documents but cannot orchestrate multistep actions; and agents are powerful but demanding—both in terms of cloud compute and engineering effort to monitor, tune, and govern. Before choosing, ask: are my inputs unstructured or unpredictable? Do I need multistep planning that adapts to intermediate results? Can a document retrieval system suffice for my users’ information needs, or must the system decide and act autonomously? Will I want this system to improve itself over time with minimal human intervention? And can I tolerate the latency and maintenance burden of a foundation model?

In short, if your task is a fixed, deterministic transformation, write some simple code. If there are a handful of known branches and you require explicit error‐handling checkpoints, use a deterministic workflow. If you primarily need natural language question‐answering over a corpus, choose a traditional chatbot or RAG architecture. But if you face high variability, open‐ended reasoning, dynamic planning needs, or continual learning requirements, invest in an autonomous agent. Making this choice thoughtfully ensures that you get the right balance of simplicity, performance, and adaptability—so your solution remains both effective and maintainable as requirements evolve.

###### **Principles for Building Effective Agentic Systems**

Creating successful autonomous agents requires an approach that prioritizes scalability, modularity, continuous learning, resilience, and future-proofing:

###### _Scalability_

Ensure that agents can handle growing workloads and diverse tasks by utilizing distributed architectures, cloud-based infrastructure, and efficient algorithms that support parallel processing and resource optimization. Example: a customer support agent that processes 10 tickets per minute may crash or hang when traffic spikes to 1,000 if not backed by autoscaling infrastructure.

###### _Modularity_

Design agents with independent, interchangeable components connected through clear interfaces. This modular approach simplifies maintenance, promotes flexibility, and facilitates rapid adaptation to new requirements or technologies. Example: a poorly modular agent that hardcodes all its tools in its agent service would require a full redeployment anytime a small addition or modification is needed to a tool.

###### _Continuous learning_

Equip agents with mechanisms to learn from experience, such as in-context learning. Integrate user feedback to refine agent behaviors and maintain

performance relevance as tasks evolve. Example: agents that ignore feedback loops may keep making the same mistakes—like misclassifying contract clauses or failing to escalate critical support issues.

###### _Resilience_

Develop robust resilience architectures capable of gracefully handling errors, security threats, timeouts, and unexpected conditions. Incorporate comprehensive error handling, stringent security measures, and redundancy to ensure reliable and continuous agent operations. Example: agents without retry or fallback logic may crash entirely when a single API call fails, leaving the user waiting and confused.

###### _Future-proofing_

Build agent systems around open standards and scalable infrastructure, fostering a culture of innovation to adapt quickly to emerging technologies and evolving user expectations. Example: tightly coupling your agent to one proprietary vendor’s prompt format can make switching models painful and limit experimentation.

Adhering to these principles enables organizations to develop autonomous agents that remain effective and relevant, adapting seamlessly to technological advancements and changing operational environments.

###### **Organizing for Success in Building Agentic Systems**

The widespread availability of foundation models via simple API calls has spurred extensive experimentation with agent systems across many organizations. Teams frequently embark on independent proofs of concept, leading to valuable discoveries and innovative ideas. However, this ease of experimentation often results in fragmentation—overlapping projects, duplicated efforts, and unfinished experiments become scattered throughout the organization. Conversely, premature standardization could stifle creativity and trap organizations into rigid frameworks or vendor-specific solutions. Achieving success requires balancing flexibility for experimentation with sufficient alignment for scalability and coherence.

In the early phases of agent development, organizations should actively encourage exploratory efforts, permitting teams to test various architectures, workflows, and models freely. Over time, as successful patterns and best practices become apparent, strategic alignment becomes critical. Implementing a “one standard per large group” strategy can effectively balance this need. Within specific departments or functional areas, teams can standardize around common tools and methodologies, streamlining collaboration without restricting broader organizational innovation.

Another essential aspect of success is avoiding vendor lock-in by adopting open standards, such as OpenAPI, and embracing modular system designs. These practices

help ensure flexibility and reduce dependency on any single technology or provider, facilitating future adaptability.

Effective knowledge sharing is also crucial. Lessons learned from both successful and unsuccessful experiments should be communicated widely via internal forums, shared repositories, and comprehensive documentation. This collaborative approach accelerates organizational learning, minimizes redundant efforts, and promotes collective improvement.

Lastly, governance frameworks should remain lightweight and flexible, emphasizing guiding principles over rigid mandates. A streamlined governance structure enables teams to innovate confidently while remaining aligned with overarching organizational objectives.

Organizing successfully around agentic systems is fundamentally iterative. Organizations must continually reassess their strategies to maintain a dynamic balance between exploration and standardization. By cultivating an environment that values experimentation, collaborative learning, and open standards, organizations can effectively transition agentic systems from isolated experiments into scalable, transformative solutions that are deeply integrated into their operational processes.

###### **Agentic Frameworks**

Numerous frameworks currently exist for developing autonomous agents, each addressing critical functionalities such as skills integration, memory management, planning, orchestration, experiential learning, and multiagent coordination. This list is certainly not exhaustive, but leading frameworks include the following.

###### **LangGraph**

###### _Strengths_

Modular orchestration framework based on directed graphs whose nodes contain discrete units of logic (often foundation model calls) and whose edges manage the flow of data through complex, potentially cyclic workflows; strong developer ergonomics; native support for asynchronous workflows and retries

###### _Trade-offs_

Requires custom logic for advanced planning and memory; less built-in support for multiagent collaboration

###### _Best for_

Teams building robust, single-agent or light multiagent systems with explicit, inspectable flow control

###### **AutoGen**

###### _Strengths_

Powerful multiagent orchestration; dynamic role assignment; flexible messagingbased interaction between agents

###### _Trade-offs_

Can be heavyweight or complex for simple use cases; more opinionated around agent interaction patterns

###### _Best for_

Research and production systems involving dialogue between multiple agents (e.g., manager-worker, self-reflection loops)

###### **CrewAI**

###### _Strengths_

Easy to learn and use; quick setup for prototyping; useful abstractions like “crew” and “tasks”

###### _Trade-offs_

Limited customization and control over orchestration internals; less mature than LangGraph or AutoGen for complex workflows

###### _Best for_

Developers who want to get started quickly on practical, human-centric agents like assistants or support agents

###### **OpenAI Agents Software Development Kit (SDK)**

###### _Strengths_

Deep integration with OpenAI’s tool ecosystem; secure and easy-to-use function calling, memory primitives, and tool routing

###### _Trade-offs_

Tightly coupled to OpenAI’s infrastructure; may be less flexible or portable for custom agent stacks or open source toolchains

###### _Best for_

Teams already using the OpenAI API and looking for a fast way to build secure, tool-using agents with minimal scaffolding

While each framework offers unique advantages and limitations, continuous innovation and competition in this space are expected to drive further evolution. For early prototypes, CrewAI or OpenAI Agents SDK can get you running quickly. For scalable, production-grade systems, LangGraph and AutoGen provide more control and sophistication. These frameworks are also not necessary, and many teams choose to build directly against the model provider APIs. This book primarily focuses on LangGraph, chosen for its straightforward yet powerful approach to agent system development. Through detailed explanations, practical examples, and real-world scenarios, we demonstrate how LangGraph effectively addresses the complexity and dynamics required by modern intelligent agents.

###### **Conclusion**

Autonomous agents represent a transformative development in AI, capable of performing complex, dynamic tasks with a high degree of autonomy. This chapter has outlined the foundational concepts of agents, highlighted their advancements over traditional ML systems, and discussed their practical applications and limitations. As we delve deeper into the design and implementation of these systems, it becomes clear that the thoughtful integration of agents into various domains holds the potential to drive significant innovation and efficiency.

While the various approaches to designing autonomous agents discussed in this chapter have demonstrated significant capabilities and potential, they also highlight the complexity and challenges involved in creating effective and adaptable systems. Each method, from rule-based systems to advanced cognitive architectures, offers unique strengths but also comes with inherent limitations. In this book, I aim to bridge these gaps.

### **CHAPTER 2 Designing Agent Systems**

Most practitioners don’t begin with a grand design document when building agent systems. They start with a messy problem, a foundation model API key, and a rough idea of what might help. This chapter is your quick start to get you up and running. We’ll cover each of the following topics in more depth through the rest of the book, and many will get their own chapter, but this chapter will give you an overview of how to design an agentic system, all grounded in a specific example of managing customer support for an ecommerce platform.

###### **Our First Agent System**

Great—you now have a working “cancel order” agent. Before we expand our agent, let’s reflect on _why_ we started with such a simple slice. Scoping is always a balancing act. If you narrow your task too much—say, only cancellations—you miss out on other high-volume requests like refunds or address changes, limiting real-world impact. But if you broaden it too far—“automate every support inquiry”—you’ll drown in edge cases like billing disputes, product recommendations, and technical troubleshooting. And if you keep it vague—“improve customer satisfaction”—you’ll never know when you’ve succeeded.

Instead, by focusing on a clear, bounded workflow—canceling orders—we ensure concrete inputs (customer message + order record), structured outputs (tool calls + confirmations), and a tight feedback loop. For example, imagine an email that says, “Please cancel my order #B73973 because I found a cheaper option elsewhere.” A human agent would look up the order, verify it hasn’t shipped, click “Cancel,” and reply with a confirmation. Translating this into code means invoking cancel_ order(order_id="B73973") and sending a simple confirmation message back to the customer.

Now that we have a working “cancel order” agent, the next question is: does it actually work? In production, we don’t just want our agent to run—we want to know how well it performs, what it gets right, and where it fails. For our cancel order agent, we care about questions like:

- Did it call the correct tool ( cancel_order )?

- Did it pass the right parameters (the correct order ID)?

- Did it send a clear, correct confirmation message to the customer?

In our open source repository, you’ll find a full evaluation script to automate this process:

- Evaluation dataset

- Batch evaluation script

Here’s a minimal, simplified version of this logic for how you might test your agent directly:

print(" ✅ Agent passed minimal evaluation.")

This snippet ensures that the tool was called and the confirmation was sent. Of course, real evaluation goes deeper: you can measure tool precision, parameter accuracy, and overall task success rates across hundreds of examples to catch edge cases before deploying. We’ll dive into evaluation strategies and frameworks in depth in Chapter 9, but for now, remember: an untested agent is an untrusted agent.

Because both steps are automated using @tool decorators, writing tests against real tickets becomes trivial—and you instantly gain measurable metrics like tool recall, parameter accuracy, and confirmation quality. Now that we’ve built and evaluated a minimal agent, let’s explore the core design decisions that will shape its capabilities and impact.

###### **Core Components of Agent Systems**

Designing an effective agent-based system requires a deep understanding of the core components that enable agents to perform their tasks successfully. Each component plays a critical role in shaping the agent’s capabilities, efficiency, and adaptability. From selecting the right models to equipping the agent with tools, memory, and planning capabilities, these elements must work together to ensure that the agent can operate in dynamic and complex environments. This section delves into the key components—the foundation model, tools, and memory—and explores how they interact to form a cohesive agent system.

###### **Model Selection**

At the heart of every agent-based system lies the model that drives the agent’s decision-making, interaction, and learning capabilities. Selecting the right model is foundational: it determines how the agent interprets inputs, generates outputs, and adapts to its environment. This decision influences the system’s performance, scalability, latency, and cost. Choosing an appropriate model depends on the complexity of the agent’s tasks, the nature of the input data, infrastructure constraints, and the trade-offs between generality, speed, and precision.

Broadly speaking, model selection starts with assessing task complexity. Large foundation models—such as GPT-5 or Claude Opus 4.1—are well suited for agents operating in open-ended environments, where nuanced understanding, flexible reasoning, and creative generation are essential. These models offer impressive generalization and excel at tasks involving ambiguity, contextual nuance, or multiple steps. However, their strengths come at a cost: they require significant computational resources, often demand cloud infrastructure, and introduce higher latency. They are best reserved for applications like personal assistants, research agents, or enterprise systems that must handle a wide range of unpredictable queries.

In contrast, smaller models—such as distilled ModernBERT variants or Phi-4—are often more appropriate for agents performing well-defined, repetitive tasks. These models run efficiently on local hardware, respond quickly, and are less expensive to deploy and maintain. They work well in structured settings like customer support, information retrieval, or data labeling, where precision is needed but creativity and flexibility are less important. When real-time responsiveness or resource constraints are critical, smaller models may outperform their larger counterparts simply by being more practical.

An increasingly important dimension in model selection is modality. Agents today often need to process not just text, but also images, audio, or structured data. Multimodal models, such as GPT-5 and Claude 4.1, enable agents to interpret and combine diverse data types—text, visuals, speech, and more. This expands the agent’s utility in domains like healthcare, robotics, and customer support, where decisions rely on integrating multiple forms of input. In contrast, text-only models remain ideal for purely language-driven use cases, offering lower complexity and faster inference in scenarios where additional modalities provide little added value.

Another key consideration is openness and customizability. Open source models, such as Llama and DeepSeek, provide developers with full transparency and the ability to fine-tune or modify the model as needed. This flexibility is particularly important for privacy-sensitive, regulated, or domain-specific applications. Open source models can be hosted on private infrastructure, tailored to unique use cases, and deployed without licensing costs—though they do require more engineering

overhead. By contrast, proprietary models like GPT-5, Claude, and Cohere offer powerful capabilities via API and come with managed infrastructure, monitoring, and performance optimizations. These models are ideal for teams seeking rapid development and deployment, though customization is often limited and costs can scale quickly with usage.

The choice between using a pretrained general-purpose model or a custom-trained model depends on the specificity and stakes of the agent’s domain. Pretrained models—trained on broad internet-scale corpora—work well for general language tasks, rapid prototyping, and scenarios where domain precision is not critical. These models can often be lightly fine-tuned or adapted through prompting techniques to achieve strong performance with minimal effort. However, in specialized domains— such as medicine, law, or technical support—custom-trained models can provide significant advantages. By training on curated, domain-specific datasets, developers can endow agents with deeper expertise and contextual understanding, leading to more accurate and trustworthy outputs.

Cost and latency considerations often tip the scales in real-world deployments. Large models deliver high performance but are expensive to run and may introduce response delays. In cases where that is untenable, smaller models or compressed versions of larger models provide a better balance. Many developers adopt hybrid strategies, where a powerful model handles the most complex queries and a lightweight model handles routine tasks. In some systems, dynamic model routing ensures that each request is evaluated and routed to the most appropriate model based on complexity or urgency—enabling systems to optimize both cost and quality.

The Center for Research on Foundation Models at Stanford University has released the Holistic Evaluation of Language Models, providing rigorous third-party performance measurement across a wide range of models. In Table 2-1, a small selection of language models are shown along with their performance on the Massive Multitask Language Understanding (MMLU) benchmark, a commonly used general assessment of these models’ abilities. These measurements are not perfect, but they provide us with a common ruler with which to compare performance. In general, we see that larger models perform better, but inconsistently (some models perform better than their size would suggest). Significantly more computation resources are required to obtain high performance.

_Table 2-1. Selected open weight models by performance and size_

Conversely, this means moderate performance can be obtained at a small fraction of the cost. As you’ll see in Table 2-1, models up to roughly 14 billion parameters can be run on a single consumer-grade graphics processing unit (GPU), such as NVIDIA’s RTX 3090 with 24 GB of video RAM. Above this threshold, though, you will probably want a server-grade GPU such as NVIDIA’s A100, which comes in 40 GB and 80 GB varieties. Models are called “open weight” when the architecture and weights (or parameters) of the model have been released freely to the public, so anyone with the necessary hardware can load and use the model for inference without paying for access. We will not get into the details of hardware selection, but these select open weight models show a range of performance levels at different sizes. These small, open weight models continue to improve at a rapid pace, bringing increasing amounts of intelligence into smaller form factors. While they might not work well for your hardest problems, they can handle easier, more routine tasks at a fraction of the price. For our example ecommerce support agent, a small fast model suffices—but if we expanded into product recommendations or sentiment-based escalation, a larger model could unlock new capabilities.

Now let’s take a look at several of the large flagship models. Note that two of these models, DeepSeek-v3 and Llama 3.1 Instruct Turbo 405B, have been released as open weight models but the others have not. That said, these large models typically require at least 12 GPUs for reasonable performance, but they can require many more. These large models are almost always used on servers in large data centers. Typically, the model trainers charge for access to these models based on the number of input and output tokens. The advantage of this is that the developer does not need to worry about servers and GPU utilization but can begin building right away. Table 2-2 shows the model costs and performance on the same MMLU benchmark.

_Table 2-2. Selected large models by performance and cost_

In Table 2-2, prices are shown as a multiple of the price per million tokens on Llama 3.1, which was the least expensive at the time of publishing. At the time of publishing, Meta is charging $0.20 per million input tokens and $0.60 per million output tokens. You might also notice that performance does not directly correlate to price. Also know that performance on benchmarks offers useful guidance, but your mileage may vary in how these benchmarks align with your particular task. When possible, compare the model for your task and find the model that provides you with the best price per performance.

Ultimately, model selection is not a onetime decision but a strategic design choice that must be revisited as agent capabilities, user needs, and infrastructure evolve. Developers must weigh trade-offs between generality and specialization, performance and cost, simplicity and extensibility. By carefully considering the task complexity, input modalities, operational constraints, and customization needs, teams can choose models that enable their agents to act efficiently, scale reliably, and perform with precision in the real world.

###### **Tools**

In agent-based systems, _tools_ are the fundamental capabilities that enable agents to perform specific actions or solve problems. Tools represent the functional building blocks of an agent, providing the ability to execute tasks and interact with both users and other systems. An agent’s effectiveness depends on the range and sophistication of its tools.

###### **Designing Capabilities for Specific Tasks**

Tools are typically tailored to the tasks that the agent is designed to solve. When designing tools, developers must consider how the agent will perform under different conditions and contexts. A well-designed toolset ensures that the agent can handle a variety of tasks with precision and efficiency. Tools can be divided into three main categories:

###### _Local tools_

These are actions that the agent performs based on internal logic and computations without external dependencies. Local tools are often rule-based or involve executing predefined functions. Examples include mathematical calculations, data retrieval from local databases, or simple decision making based on

predefined rules (e.g., deciding whether to approve or deny a request based on set criteria).

###### _API-based tools_

API-based tools enable agents to interact with external services or data sources. These tools enable agents to extend their capabilities beyond the local environment by fetching real-time data or leveraging third-party systems. For instance, a virtual assistant might use an API to pull weather data, stock prices, or social media updates, enabling it to provide more contextual and relevant responses to user queries.

###### _Model Context Protocol (MCP)_

MCP-based tools enable agents to provide structured, real-time context to language models using the Model Context Protocol, a standardized schema for passing external knowledge, memory, and state into the model’s prompt. Unlike traditional API calls that require full round-trip execution, MCP enables agents to inject rich, dynamic context—such as user profiles, conversation history, world state, or task-specific metadata—directly into the model’s reasoning process without invoking separate tools. They are particularly effective in reducing redundant tool use, preserving conversational state, and injecting real-time situational awareness into model behavior.

While local tools enable agents to perform tasks independently using internal logic and rule-based functions, such as calculations or data retrieval from local databases, API-based tools enable agents to connect with external services. This allows for the access of real-time data or third-party systems to provide contextually relevant responses and extended functionality.

###### **Tool Integration and Modularity**

Modular design is critical for tool development. Each tool should be designed as a self-contained module that can be easily integrated or replaced as needed. This approach enables developers to update or extend the agent’s functionality without overhauling the entire system. A customer service chatbot might start with a basic set of tools for handling simple queries and later have more complex tools (e.g., dispute resolution or advanced troubleshooting) added without disrupting the agent’s core operations.

###### **Memory**

Memory is an essential component that enables agents to store and retrieve information, enabling them to maintain context, learn from past interactions, and improve decision making over time. Effective memory management ensures that agents can

operate efficiently in dynamic environments and adapt to new situations based on historical data. We’ll discuss memory in much more detail in Chapter 6.

###### **Short-Term Memory**

Short-term memory refers to an agent’s ability to store and manage information relevant to the current task or conversation. This type of memory is typically used to maintain context during an interaction, enabling the agent to make coherent decisions in real time. A customer service agent that remembers a user’s previous queries within a session can provide more accurate and context-aware responses, enhancing user experience.

Short-term memory is often implemented using _rolling context windows_ , which enable the agent to maintain a sliding window of recent information while discarding outdated data. This is particularly useful in applications like chatbots or virtual assistants, where the agent must remember recent interactions but can forget older, irrelevant details.

###### **Long-Term Memory**

Long-term memory, on the other hand, enables agents to store knowledge and experiences over extended periods, enabling them to draw on past information to inform future actions. This is particularly important for agents that need to improve over time or provide personalized experiences based on user preferences.

Long-term memory is often implemented using databases, knowledge graphs, or fine-tuned models. These structures enable agents to store structured data (e.g., user preferences, historical performance metrics) and retrieve it when needed. A healthcare monitoring agent might retain long-term data on a patient’s vital signs, enabling it to detect trends or provide historical insights to healthcare providers.

###### **Memory Management and Retrieval**

Effective memory management involves organizing and indexing stored data so that it can be easily retrieved when needed. Agents that rely on memory must be able to differentiate between relevant and irrelevant data and retrieve information quickly to ensure seamless performance. In some cases, agents may also need to forget certain information to avoid cluttering their memory with outdated or unnecessary details.

An ecommerce recommendation agent must store user preferences and past purchase history to provide personalized recommendations. However, it must also prioritize recent data to ensure that recommendations remain relevant and accurate as user preferences change over time.

###### **Orchestration**

Orchestration is what turns isolated capabilities into end-to-end solutions: it’s the logic that composes, schedules, and supervises a series of skills so that each action flows into the next and works toward a clear objective. At its core, orchestration evaluates possible sequences of tool or skill invocations, forecasts their likely outcomes, and picks the path most likely to succeed in multistep tasks—whether that’s plotting an optimal delivery route that balances traffic, time windows, and vehicle availability, or assembling a complex data-processing pipeline.

Because real-world conditions can change in an instant—new information arrives, priorities shift, or resources become unavailable—an orchestrator must continuously monitor both progress and environment, pausing or rerouting workflows as needed to stay on course. In many scenarios, agents build plans incrementally: they execute a handful of steps, then reassess and update the remaining workflow based on fresh results. A conversational assistant, for example, might confirm each subtask’s outcome before planning the next, dynamically adapting its sequence to ensure responsiveness and robustness.

Without a solid orchestration layer, even the most powerful skills risk running at cross-purposes or stalling entirely. We’ll dig into the patterns, architectures, and best practices for building resilient, flexible orchestration engines in Chapter 5.

###### **Design Trade-Offs**

Designing agent-based systems involves balancing multiple trade-offs to optimize performance, scalability, reliability, and cost. These trade-offs require developers to make strategic decisions that can significantly impact how the agent performs in realworld environments. This section explores the critical trade-offs involved in creating effective agent systems and provides guidance on how to approach these challenges.

###### **Performance: Speed/Accuracy Trade-Offs**

A key trade-off in agent design is balancing speed and accuracy. High performance often enables an agent to quickly process information, make decisions, and execute tasks, but this can come at the expense of precision. Conversely, focusing on accuracy can slow the agent down, particularly when complex models or computationally intensive techniques are required.

In real-time environments, such as autonomous vehicles or trading systems, rapid decision making is essential, with milliseconds sometimes making a critical difference; here, prioritizing speed over accuracy may be necessary to ensure timely responses. However, tasks like legal analysis or medical diagnostics require high precision, making it acceptable to sacrifice some speed to ensure reliable results.

A hybrid approach can also be effective, where an agent initially provides a fast, approximate response and then refines it with a more accurate follow-up. This approach is common in recommendation systems or diagnostics, where a quick initial suggestion is validated and improved with additional time and data.

###### **Scalability: Engineering Scalability for Agent Systems**

Scalability is a critical challenge for modern agent-based systems, especially those that rely heavily on deep learning models and real-time processing. As agent systems grow in complexity, data volume, and task concurrency, it becomes critical to manage computational resources, particularly GPUs. GPUs are the backbone for accelerating the training and inference of large AI models, but efficient scaling requires careful engineering to avoid bottlenecks, underutilization, and rising operational costs. This section outlines strategies for effectively scaling agent systems by optimizing GPU resources and architecture.

GPU resources are often the most expensive and limiting factor in scaling agent systems, making their efficient use a top priority. Proper resource management enables agents to handle increasing workloads while minimizing the latency and cost associated with high-performance computing. A critical strategy for scalability is dynamic GPU allocation, which involves assigning GPU resources based on real-time demand. Instead of statically allocating GPUs to agents or tasks, dynamic allocation ensures that GPUs are only used when necessary, reducing idle time and optimizing utilization.

Elastic GPU provisioning further enhances efficiency, using cloud services or onpremises GPU clusters that automatically scale resources based on current workloads.

Priority queuing and intelligent task scheduling add another layer of efficiency, giving high-priority tasks immediate GPU access while queuing less critical ones during peak times.

In large-scale agent systems, latency can become a significant issue, particularly when agents need to interact in real-time or near-real-time environments. Optimizing for minimal latency is essential for ensuring that agents remain responsive and capable of meeting performance requirements. Scheduling GPU tasks efficiently across distributed systems can reduce latency and ensure that agents operate smoothly under heavy loads.

One effective strategy is asynchronous task execution, which enables GPU tasks to be processed in parallel without waiting for previous tasks to be completed, maximizing GPU resource utilization and reducing idle time between tasks.

Another strategy is dynamic load balancing across GPUs, which prevents any single GPU from becoming a bottleneck by distributing tasks to underutilized resources. For agent systems reliant on GPU-intensive tasks, such as running complex inference

algorithms, scaling effectively requires more than simply adding GPUs; it demands careful optimization to ensure that resources are fully utilized, enabling the system to meet growing demands efficiently.

To scale GPU-intensive systems effectively, it requires more than just adding GPUs— it involves ensuring that GPU resources are fully utilized and that the system can scale efficiently as demands grow.

Horizontal scaling involves expanding the system by adding more GPU nodes to handle increasing workloads. In a cluster setup, GPUs can work together to manage highvolume tasks such as real-time inference or model training.

For agent systems with varying workloads, using a hybrid cloud approach can improve scalability by combining on-premises GPU resources with cloud-based GPUs. During peak demand, the system can use burst scaling, in which tasks are offloaded to temporary cloud GPUs, scaling up computational capacity without requiring a permanent investment in physical infrastructure. Once demand decreases, these resources can be released, ensuring cost-efficiency.

Using cloud-based GPU instances during off-peak hours, when demand is lower and pricing is more favorable, can significantly reduce operating costs while maintaining the flexibility to scale up when needed.

Scaling agent systems effectively—particularly those reliant on GPU resources— requires a careful balance between maximizing GPU efficiency, minimizing latency, and ensuring that the system can handle dynamic workloads. By adopting strategies such as dynamic GPU allocation, multi-GPU parallelism, distributed inference, and hybrid cloud infrastructures, agent systems can scale to meet growing demands while maintaining high performance and cost efficiency. GPU resource management tools play a critical role in this process, providing the oversight necessary to ensure seamless scalability as agent systems grow in complexity and scope.

###### **Reliability: Ensuring Robust and Consistent Agent Behavior**

_Reliability_ refers to the agent’s ability to perform its tasks consistently and accurately over time. A reliable agent must handle expected and unexpected conditions without failure, ensuring a high level of trust from users and stakeholders. However, improving reliability often involves trade-offs in system complexity, cost, and development time.

###### **Fault tolerance**

One key aspect of reliability is ensuring that agents can handle errors or unexpected events without crashing or behaving unpredictably. This may involve building in _fault tolerance_ , where the agent can detect failures (e.g., network interruptions, hardware — failures) and recover gracefully. Fault-tolerant systems often employ _redundancy_

duplicating critical components or processes to ensure that failures in one part of the system do not affect overall performance.

###### **Consistency and robustness**

For agents to be reliable, they must perform consistently across different scenarios, inputs, and environments. This is particularly important in safety-critical systems, such as autonomous vehicles or healthcare agents, where a mistake could have serious consequences. Developers must ensure that the agent performs well not only in ideal conditions but also under edge cases, stress tests, and real-world constraints. Achieving reliability requires:

###### _Extensive testing_

Agents should undergo rigorous testing, including unit tests, integration tests, and simulations of real-world scenarios. Tests should cover edge cases, unexpected inputs, and adversarial conditions to ensure that the agent can handle diverse environments.

###### _Monitoring and feedback loops_

Reliable agents require continuous monitoring in production to detect anomalies and adjust their behavior in response to changing conditions. Feedback loops enable agents to learn from their environment and improve performance over time, increasing their robustness.

###### **Costs: Balancing Performance and Expense**

Cost is an often-overlooked but critical trade-off in the design of agent-based systems. The costs associated with developing, deploying, and maintaining an agent must be weighed against the expected benefits and return on investment (ROI). Cost considerations affect decisions related to model complexity, infrastructure, and scalability.

###### **Development costs**

Developing sophisticated agents can be expensive, especially when using advanced machine learning (ML) models that require large datasets, specialized expertise, and significant computational resources for training. Additionally, the need for iterative design, testing, and optimization increases development costs.

Complex agents frequently necessitate a team with specialized talent, including data scientists, ML engineers, and domain experts, to create high-performing systems. Additionally, building a reliable and scalable agent system requires extensive testing infrastructure, often involving simulation environments and investments in testing tools and frameworks to ensure robust functionality.

###### **Operational costs**

After deployment, the operational costs of running agents can become substantial, particularly for systems requiring high computational power, such as those involving real-time decision making or continuous data processing. Key contributors to these expenses include the need for significant compute power, as agents running deep learning models or complex algorithms often rely on costly hardware like GPUs or cloud services.

Additionally, agents that process vast amounts of data or maintain extensive memory incur higher costs for data storage and bandwidth. Regular maintenance and updates, including bug fixes and system improvements, further add to operational expenses as resources are needed to ensure the system’s reliability and performance over time.

###### **Cost versus value**

Ultimately, the cost of an agent-based system must be justified by the value it delivers. In some cases, it may make sense to prioritize cheaper, simpler agents for less critical tasks, while investing heavily in more sophisticated agents for mission-critical applications. Decisions around cost must be made in the context of the system’s overall goals and expected lifespan. Some optimization strategies include:

###### _Lean models_

Using simpler, more efficient models where appropriate can help reduce both development and operational costs. For example, if a rule-based system can achieve similar results to a deep learning model for a given task, the simpler approach will often be more cost-effective.

###### _Cloud-based resources_

Leveraging cloud computing resources can reduce up-front infrastructure costs, establishing a more scalable, pay-as-you-go model.

###### _Open source models and tools_

Utilizing open source ML libraries and frameworks can help minimize software development costs while still delivering high-quality agents.

Designing agent systems involves balancing several critical trade-offs. Prioritizing performance may require sacrificing some accuracy, while scaling to a multiagent architecture introduces challenges in coordination and consistency. Ensuring reliability demands rigorous testing and monitoring but can increase development time and complexity. Finally, cost considerations must be factored in from both a development and operational perspective, ensuring that the system delivers value within budget constraints. In the next section, we’ll review some of the most common design patterns used when building effective agentic systems.

###### **Architecture Design Patterns**

The architectural design of agent-based systems determines how agents are structured, how they interact with their environment, and how they perform tasks. The choice of architecture influences the system’s scalability, maintainability, and flexibility. This section explores three common design patterns for agent-based systems— single-agent and multiagent architectures—and discusses their advantages, challenges, and appropriate use cases. We’ll discuss this in far more detail in Chapter 8.

###### **Single-Agent Architectures**

A single-agent architecture is among the simplest and most straightforward designs, where a single agent is responsible for managing and executing all tasks within a system. This agent interacts directly with its environment and independently handles decision making, planning, and execution without relying on other agents.

Ideal for well-defined and narrow tasks, this architecture is best suited for workloads that are manageable by a single entity. The simplicity of single-agent systems makes them easy to design, develop, and deploy, as they avoid complexities related to coordination, communication, and synchronization across multiple components. With clear use cases, single-agent architectures excel in narrow-scope tasks that do not require collaboration or distributed efforts, such as simple chatbots handling basic customer queries (like FAQs and order tracking) and task-specific automation for data entry or file management.

Single-agent setups work well in environments where the problem domain is welldefined, tasks are straightforward, and there is no significant need for scaling. This makes them a fit for customer service chatbots, general-purpose assistants, and code generation agents. We’ll discuss single-agent and multiagent architectures much more in Chapter 8.

###### **Multiagent Architectures: Collaboration, Parallelism, and Coordination**

In multiagent architectures, multiple agents work together to achieve a common goal. These agents may operate independently, in parallel, or through coordinated efforts, depending on the nature of the tasks. Multiagent systems are often used in complex environments where different aspects of a task need to be managed by specialized agents or where parallel processing can improve efficiency and scalability, and they bring many advantages:

###### _Collaboration and specialization_

Each agent in a multiagent system can be designed to specialize in specific tasks or areas. For example, one agent may focus on data collection while another

processes the data, and a third agent manages user interactions. This division of labor enables the system to handle complex tasks more efficiently than a single agent would.

###### _Parallelism_

Multiagent architectures can leverage parallelism to perform multiple tasks simultaneously. For instance, agents in a logistics system can simultaneously plan different delivery routes, reducing overall processing time and improving efficiency.

###### _Improved scalability_

As the system grows, additional agents can be introduced to handle more tasks or to distribute the workload. This makes multiagent systems highly scalable and capable of managing larger and more complex environments.

###### _Redundancy and resilience_

Because multiple agents operate independently, failure in one agent does not necessarily compromise the entire system. Other agents can continue to function or even take over the failed agent’s responsibilities, improving overall system reliability.

Despite these advantages, multiagent systems also come with significant challenges, which include:

###### _Coordination and communication_

Managing communication between agents can be complex. Agents must exchange information efficiently and coordinate their actions to avoid duplication of efforts, conflicting actions, or resource contention. Without proper orchestration, multiagent systems can become disorganized and inefficient.

###### _Increased complexity_

While multiagent systems are powerful, they are also more challenging to design, develop, and maintain. The need for communication protocols, coordination strategies, and synchronization mechanisms adds layers of complexity to the system architecture.

###### _Lower efficiency_

While not always the case, multiagent systems often encounter reduced efficiency due to higher token consumption when completing tasks. Because agents must frequently communicate, share context, and coordinate actions, they consume more processing power and resources compared with single-agent systems. This increased token usage not only leads to higher computational costs but can also slow task completion if communication and coordination are not optimized. Consequently, while multiagent systems offer robust solutions for complex tasks, their efficiency challenges mean that careful resource management is crucial.

Multiagent architectures are well suited for environments where tasks are complex, distributed, or require specialization across different components. In these systems, multiple agents contribute to solving complex, distributed problems, such as in financial trading systems, cybersecurity investigations, or collaborative AI research platforms.

Single-agent systems offer simplicity and are ideal for well-defined tasks. Multiagent systems provide collaboration, parallelism, and scalability, making them suitable for complex environments. Choosing the right architecture depends on the complexity of the task, the need for scalability, and the expected lifespan of the system. In the next section, we’ll discuss some principles we can follow to get the best results from the agentic systems we build.

###### **Best Practices**

Designing agent-based systems requires more than just building agents with the right models, skills, and architecture. To ensure that these systems perform optimally in real-world conditions and continue to evolve as the environment changes, it’s essential to follow best practices throughout the development lifecycle. This section highlights three critical best practices— _iterative design_ , _evaluation strategy_ , and _real-world testing_ —that contribute to creating adaptable, efficient, and reliable agent systems.

###### **Iterative Design**

Iterative design is a fundamental approach in agent development, emphasizing the importance of building systems incrementally while continually incorporating feedback. Instead of aiming for a perfect solution in the initial build, iterative design focuses on creating small, functional prototypes that you can evaluate, improve, and refine over multiple cycles. This process allows for quick identification of flaws, rapid course correction, and continuous system improvement, and it has multiple benefits:

###### _Early detection of issues_

By releasing early prototypes, developers can identify design flaws or performance bottlenecks before they become deeply embedded in the system. This enables swift remediation of issues, reducing long-term development costs and avoiding major refactors.

###### _User-centric design_

Iterative design encourages frequent feedback from stakeholders, end users, and other developers. This feedback ensures that the agent system remains aligned with the users’ needs and expectations. As agents are tested in real-world scenarios, iterative improvements can fine-tune their behaviors and responses to better suit the users they serve.

###### _Scalability_

Starting with a minimal viable product (MVP) or basic agent enables the system to grow and evolve in manageable increments. As the system matures, new features and capabilities can be introduced gradually, ensuring that each addition is thoroughly tested before full deployment.

To adopt iterative design effectively, development teams should:

###### _Develop prototypes quickly_

Focus on building core functionality first. Don’t aim for perfection at this stage— build something that works and delivers value, even if it’s basic.

###### _Test and gather feedback_

After each iteration, collect feedback from users, developers, and other stakeholders. Use this feedback to guide improvements and decide on the next iteration’s priorities.

###### _Refine and repeat_

Based on feedback and performance data, make necessary changes and refine the system in the next iteration. Continue this cycle until the agent system meets its performance, usability, and scalability goals.

Effective iterative design involves quickly developing functional prototypes, gathering feedback after each iteration, and continuously refining the system based on insights to meet performance and usability goals.

###### **Evaluation Strategy**

Evaluating the performance and reliability of agent-based systems is a critical part of the development process. A robust evaluation ensures that agents are capable of handling real-world scenarios, performing under varying conditions, and meeting performance expectations. It involves a systematic approach to testing and validating agents across different dimensions, including accuracy, efficiency, robustness, and scalability. This section explores key strategies for creating a comprehensive evaluation framework for agent systems. We’ll cover measurement and validation in far more depth in Chapter 9.

A robust evaluation process involves developing a comprehensive testing framework that covers all aspects of the agent’s functionality. This framework ensures that the agent is thoroughly tested under a variety of scenarios, both expected and unexpected.

Functional testing focuses on verifying that the agent performs its core tasks correctly. Each skill or module of the agent should be individually tested to ensure that it behaves as expected across different inputs and scenarios. Key areas of focus include:

###### _Correctness_

Ensuring that the agent consistently delivers accurate and expected outputs based on its design

###### _Boundary testing_

Evaluating how the agent handles edge cases and extreme inputs, such as very large datasets, unusual queries, or ambiguous instructions

###### _Task-specific metrics_

For agents handling domain-specific tasks (e.g., legal analysis, medical diagnostics), ensuring the system meets the domain’s accuracy and compliance requirements

For agent systems, particularly those powered by ML models, it is essential to evaluate the agent’s ability to generalize beyond the specific scenarios it was trained on. This ensures the agent can handle new, unseen situations while maintaining accuracy and reliability.

Agents often encounter tasks outside of their original training domain. A robust evaluation should test the agent’s ability to adapt to these new tasks without requiring extensive retraining. This is particularly important for general-purpose agents or those designed to operate in dynamic environments.

User experience is a key factor in determining the success of agent systems. It’s important to evaluate not only the technical performance of the agent but also how well it meets user expectations in real-world applications.

Collecting feedback from actual users provides critical insights into how well the agent performs in practice. This feedback helps refine the agent’s behaviors, improving its effectiveness and user satisfaction, and can consist of the following:

###### _User satisfaction scores_

Use metrics like net promoter score (NPS) or customer satisfaction (CSAT) to gauge how users feel about their interactions with the agent.

###### _Task completion rates_

Measure how often users successfully complete tasks with the agent’s help. Low completion rates may indicate confusion or inefficiencies in the agent’s design.

###### _Explicit signals_

Create opportunities for users to provide their feedback, in such forms as thumbs-up and thumbs-down, star ratings, and the ability to accept, reject, or modify the generated results, depending on the context. These signals can provide a wealth of insight.

###### _Implicit signals_

Analyze user-agent interactions to identify common points of failure, such as misinterpretations, delays, sentiment, or inappropriate responses. Interaction logs can be mined for insights into areas where the agent needs improvement.

In some cases, it’s necessary to involve human experts in the evaluation process to assess the agent’s decision-making accuracy. Human-in-the-loop validation combines automated evaluation with human judgment, ensuring that the agent’s performance aligns with real-world standards. When feasible, human experts should review a sample of the agent’s outputs to verify correctness, ethical compliance, and alignment with best practices, and these reviews can then be used to calibrate and improve automated evaluations.

We should evaluate agents in environments that closely simulate their real-world applications. This helps ensure that the system can perform reliably outside of controlled development conditions. Evaluate the agent across the full spectrum of its operational environment, from data ingestion and processing to task execution and output generation. End-to-end testing ensures that the agent functions as expected across multiple systems, data sources, and platforms.

###### **Real-World Testing**

While building agents in a controlled development environment is crucial for initial testing, it’s equally important to validate agents in real-world settings to ensure they perform as expected when interacting with live users or environments. Real-world testing involves deploying agents in actual production environments and observing their behavior under real-life conditions. This stage of testing enables developers to uncover issues that may not have surfaced during earlier development stages and to evaluate the agent’s robustness, reliability, and user impact.

Real-world testing is essential for ensuring agents can manage the unpredictability and complexity of live environments. Unlike controlled testing, this approach reveals edge cases, unexpected user inputs, and performance under high demand, helping developers refine the agent for robust, reliable operation:

###### _Exposure to real-world complexity_

In controlled environments, agents operate with predictable inputs and responses. However, real-world environments are dynamic and unpredictable, with diverse users, edge cases, and unforeseen challenges. Testing in these environments ensures that the agent can handle the complexity and variability of realworld scenarios.

###### _Uncovering edge cases_

Real-world interactions often expose edge cases that may not have been accounted for in the design or testing phases. For example, a chatbot tested with scripted

queries might perform well in development, but when exposed to real users, it may struggle with unexpected inputs, ambiguous questions, or natural language variations.

###### _Evaluating performance under load_

Real-world testing also enables developers to observe how the agent performs under high workloads or increased user demand. This is particularly important for agents that operate in environments with fluctuating traffic, such as customer service bots or ecommerce recommendation engines.

Real-world testing ensures an agent’s readiness for deployment by validating its performance under real-life conditions. This process involves a phased rollout, continuous monitoring of key metrics, collecting user feedback, and iteratively refining the agent to optimize its capabilities and usability:

###### _Deploy in phases_

Roll out the agent in stages, starting with small-scale testing in a limited environment before scaling up to full deployment. This phased approach helps identify and address issues incrementally, without overwhelming the system or users.

###### _Monitor agent behavior_

Use monitoring tools to track the agent’s behavior, responses, and performance metrics during real-world testing. Monitoring should focus on key performance indicators (KPIs) such as response time, accuracy, user satisfaction, and system stability.

###### _Collect user feedback_

Engage users during real-world testing to gather feedback on their experiences when interacting with the agent. User feedback is invaluable in identifying gaps, improving usability, and ensuring that the agent meets real-world needs.

###### _Iterate based on insights_

Real-world testing provides valuable insights that should be fed back into the development cycle. Use these insights to refine the agent, improve its capabilities, and optimize its performance for future iterations.

Following best practices such as iterative design, agile development, and real-world testing is critical for building agent-based systems that are adaptable, scalable, and resilient. These practices ensure that agents are designed with flexibility, thoroughly tested in real-world conditions, and continuously improved to meet evolving user needs and environmental challenges. By incorporating these approaches into the development lifecycle, developers can create more reliable, efficient, and effective agent systems capable of thriving in dynamic environments.

###### **Conclusion**

You don’t need a 30-page plan to start building a good agent system—but a little foresight goes a long way. As we saw with our ecommerce support agent, picking a tractable slice—like canceling orders—lets you build something small, testable, and immediately useful. Define what success looks like, avoid vague or over-scoped ambitions, and focus on delivering clear value quickly.

Effective agent systems are more than a sum of their parts. They depend on strong architecture, disciplined engineering, and tight feedback loops. Choosing the right structural pattern sets the stage for scalability and resilience, while iterative development and robust evaluation ensure your agents improve over time. Best practices like phased rollouts and real-world testing turn promising prototypes—like our simple cancel order agent—into reliable systems that can be trusted in production.

In Chapter 3, we shift focus to the human side of the equation—how to design agent experiences that are clear, responsive, and intuitive for the people who rely on them. Ultimately, no matter how powerful your system architecture, its success depends on how it lands in human hands.

### **CHAPTER 3 User Experience Design for Agentic Systems**

As agent systems become an integral part of our digital environments—whether through chatbots, virtual assistants, or fully autonomous workflows—the user experience (UX) they deliver plays a pivotal role in their success. While foundation models and agent architectures enable remarkable technical capabilities, how users interact with these agents ultimately determines their effectiveness, trustworthiness, and adoption. A well-designed agent experience not only empowers users but also builds confidence, minimizes frustration, and ensures clarity in agent capabilities and limitations. The field of agent UX is evolving at an unprecedented pace. New interface paradigms, modality combinations, and user interaction models are emerging almost monthly. This chapter provides foundational design principles that remain relevant even as the specific technologies and capabilities continue to advance rapidly. Designing UX for agent systems introduces unique challenges and opportunities. Agents can interact through a variety of modalities, including text, graphical interfaces, speech, and even video.

_Table 3-1. Placeholder_

Another key UX consideration is how the context is managed over time. Some generative AI applications have no memory or learning, so have precisely the information you present them with in exactly that session. This requires users to copy and paste information into the prompt. More modern applications automatically manage this context for you. For example, Cursor uses the integrated development environment to intelligently identify code to include in each model inference. Some applications retain memory over time, enabling agents to remember past interactions, maintain conversation flow, and adapt to user preferences over time. Without these capabilities, even technically advanced agents risk feeling disjointed or unresponsive. Similarly, communicating agent capabilities, limitations, and uncertainty is essential for setting realistic user expectations and preventing misunderstandings. Users must know what an agent can and cannot do, and when they might need to intervene or provide guidance.

Finally, trust and transparency remain foundational to positive user experiences with agent systems. Predictable agent behavior and clear explanations of actions contribute to building relationships where users feel confident relying on agents in highstakes scenarios.

This chapter explores these core aspects of UX design for agentic systems, offering principles, best practices, and actionable insights to help you design interactions that are intuitive, reliable, and aligned with user needs. Whether you’re building a chatbot, an AI-powered personal assistant, or a fully autonomous workflow agent, the principles in this chapter will help you create meaningful and effective experiences that users can trust.

###### **Interaction Modalities**

Agent systems interact with users through a variety of modalities, each offering unique strengths, limitations, and design considerations. Whether through text, graphical interfaces, speech, or video, the choice of modality shapes how users perceive and interact with agents. Text-based interfaces excel in clarity and traceability; graphical interfaces offer visual richness and intuitive controls; voice interactions provide hands-free convenience; and video interfaces enable dynamic, real-time communication.

In the next section, we’ll explore these interaction modalities, examining their key strengths, challenges, and best practices for delivering exceptional UX in agent systems.

###### **Text-Based**

Text-based interfaces are one of the most common and versatile ways users interact with agent systems—found in everything from customer service chatbots and command-line tools to productivity assistants integrated into messaging platforms. Their widespread adoption can be attributed to their simplicity, familiarity, and ease of integration into existing workflows. Text interfaces offer a unique advantage: they can support both synchronous conversations (in real time) and asynchronous interactions (where users can return to the conversation at their convenience without losing context). Additionally, text interactions create a clear and traceable record of exchanges, enabling transparency, accountability, and easier troubleshooting when something goes wrong.

In recent years, the text-based modality has undergone a renaissance driven by the integration of advanced AI capabilities within terminal environments. Tools like Warp, Claude Code, and Gemini CLI illustrate this shift vividly. Warp reimagines the traditional developer terminal by integrating natural language command translation, intelligent autocompletion, and context-aware explanations, turning the command line into a collaborative, AI-augmented workspace. To illustrate this trend,. This demonstration captures how developers can interact with the terminal using natural language prompts to generate, run, and debug commands seamlessly, without memorizing complex syntax or flags.

Similarly, Claude Code and Gemini CLI extend natural language interactions to code generation, execution, and file manipulation directly within terminal workflows, enabling developers to perform complex tasks by simply describing their goals in plain English. This figure highlights how AI is revitalizing the humble terminal, transforming it from a tool accessible only to those with deep command-line expertise into an approachable, powerful gateway for both novice and expert users to interact with systems through natural language.

This trend reflects a broader rethinking of what text-based interfaces can achieve. The incredible natural language understanding capabilities of modern foundation models are making ordinary text-based interactions more powerful than ever before. Where traditional terminals required precise syntax knowledge and memorization of command flags, AI terminals now act as conversational partners, interpreting user intent, suggesting best practices, and even debugging errors in real time. This shift is democratizing access to powerful systems operations, scripting, and data workflows, making the terminal “new again” as an accessible, intelligent gateway for both novice and expert users.

However, a key limitation of text-based interfaces is discoverability. Users often do not know what capabilities the agent supports or how to phrase commands effectively. Unlike graphical interfaces—where options, buttons, and menus visually indicate what actions are possible—text-based interfaces require users to guess or recall available functionalities. This lack of affordances can lead to confusion, underutilization of agent capabilities, and user frustration when their requests fall outside the agent’s supported scope. For example, a user might ask a support chatbot to modify an order detail that the system does not support, receiving an opaque rejection rather than guidance toward what is possible.

Designing effective text-based agents therefore requires strategies to enhance discoverability. Agents should proactively communicate their supported functions, either through onboarding messages, periodic capability reminders, or dynamic suggestions during conversation. For instance, an agent can respond to a greeting not only with “How can I help you today?” but also with “I can help you cancel orders, check delivery status, or update your account details.” This approach ensures users understand the agent’s operational boundaries, reducing trial-and-error interactions.

Beyond discoverability, text-based design requires careful attention to clarity, context retention, and error management. Agents should communicate with concise and unambiguous responses, avoiding overly technical jargon or long-winded explanations that may overwhelm the user. Maintaining context across multiturn conversations is equally important; users should not need to repeat themselves or clarify past instructions. Effective agents are also graceful in failure, providing clear error messages and fallback mechanisms, such as escalating to a human operator or offering alternative suggestions when they cannot fulfill a request. Turn-taking management is another subtle but crucial element—agents must guide conversations naturally, balancing when to ask follow-up questions and when to pause for user input.

Ambiguity in natural language remains a significant hurdle, as users may phrase requests in unexpected ways, requiring robust intent recognition to avoid misunderstandings. Additionally, text-based agents are often constrained by response length limits—too short, and they risk being cryptic; too long, and they risk overwhelming or frustrating the user. Emotional nuance is another limitation. Without vocal tone, facial expressions, or visual cues, text-based agents must rely on carefully crafted language to ensure they convey empathy, friendliness, or urgency where appropriate.

Despite these challenges, text-based agents shine in scenarios where precision, traceability, and asynchronous communication are valuable. They excel in customer support, where chatbots provide quick answers to frequently asked questions, or in productivity tools, where command-line interfaces help users execute tasks efficiently. They are equally effective in knowledge retrieval systems, answering specific questions or pulling data from structured databases.

When designed thoughtfully, text-based agents are reliable, adaptable, and deeply useful across a wide range of contexts. For example, text-based agents might be ideal for chat interfaces over messaging apps—like Slack, Teams, and WhatsApp for scalable communications with customers or employees—or text-heavy workloads like customer service, claims processing, or textual research tasks. Their accessibility and ease of deployment make them a cornerstone of agentic UX design—provided their limitations (particularly around discoverability) are mitigated through clear communication of capabilities, robust error handling, and a focus on seamless conversational flow.

###### **Graphical Interfaces**

Graphical interfaces offer users a visual and interactive way to engage with agent systems, combining text, buttons, icons, and other graphical elements to facilitate communication. These interfaces are particularly effective for tasks requiring visual clarity, structured workflows, or multistep processes, where pure text or voice interactions may fall short. Common examples include dashboard-based AI tools, graphical chat interfaces, and agent-powered productivity platforms with clickable elements.

The key strength of graphical interfaces lies in their ability to present information visually and reduce cognitive load. Humans primarily rely on visual input and can process visual information more quickly and easily than text-based information. Welldesigned interfaces can display complex data, status updates, or task progress in an intuitive and digestible format. Visual cues, such as progress bars, color coding, and alert icons, guide users effectively without requiring lengthy explanations.

For example, an agent managing a workflow might use a dashboard to show pending tasks, completed steps, and error notifications, enabling users to quickly understand the system’s state at a glance. Tools like LangSmith, n8n, Arize, and AutoGen are beginning to illustrate agent workflows visually, making them easier to understand, debug, and reason about; we are likely to see much more of this visual orchestration in the future. To see how these graphical orchestration interfaces are emerging in practice,. Tools like this illustrate agent actions, tool calls, conditionals, and outputs as connected visual nodes, enabling developers and operators to easily understand, debug, and optimize complex agentic flows without stepping through raw code alone.

. These environments integrate natural language understanding directly into the coding workflow, enabling developers to ask questions, generate code, refactor functions, and receive explanations or performance optimizations—all within a single, streamlined graphical interface.

Together, these examples illustrate the rapid evolution of graphical agentic UX. As these interfaces mature, they will redefine what productive, AI-enabled tools look like —not just for developers, but for every knowledge-intensive profession.

A growing frontier in graphical agent interfaces is the emergence of generative UIs. Instead of relying solely on static dashboards or predesigned layouts, generative UIs dynamically create interface elements, data visualizations, or structured outputs based on user queries. For example, Perplexity AI not only provides textual answers but also generates structured knowledge cards, reference lists, and data tables tailored to the question asked. Similarly, AI coding copilots generate entire forms, config files, or UI components based on user intent.

Generative UIs combine the flexibility of natural language with the clarity and discoverability of graphical layouts, enabling agents to create rich, context-specific interfaces on demand. This expands the usefulness of graphical agents from predefined workflows to open-ended tasks where visual structuring enhances understanding. However, designing generative UIs introduces new challenges: ensuring the generated elements are usable and aesthetically coherent, and that they do not overwhelm users with poorly organized or excessive information. Careful design patterns, layout constraints, and prioritization logic are critical to keep generative UIs effective and userfriendly.

Designing effective graphical agent interfaces also comes with traditional challenges. Screen real estate is limited, requiring prioritization of displayed information to ensure critical details are not buried in clutter. Agents must manage interface responsiveness—users expect real-time updates and smooth transitions between states, especially when agents operate asynchronously. Additionally, graphical elements must adapt gracefully across devices and screen sizes, ensuring consistency whether viewed on a desktop, tablet, or mobile phone.

Another critical consideration is the balance between automation and user control. Graphical interfaces often blend agent autonomy with user-driven actions, such as approving agent-suggested decisions or manually overriding recommendations. For example, an agent suggesting a calendar change might display multiple options through buttons, giving users a clear and efficient way to make a final decision.

Graphical interfaces excel in use cases where data visualization, structured interactions, and clear status updates are essential. Examples include task management dashboards, data analytics tools powered by AI agents, ecommerce product recommendation systems with filters and visual previews, and generative UI systems that dynamically produce structured outputs tailored to user questions. They are particularly effective in hybrid workflows where agents operate in the background but present updates or options visually for user confirmation.

When implemented thoughtfully, graphical and generative interfaces enable clear, efficient, and satisfying interactions with agents. They reduce ambiguity, improve task clarity, and offer users a tangible sense of control. By focusing on clarity, responsiveness, intuitive design patterns, and the emerging potential of generative UI capabilities, graphical interfaces ensure that agent interactions feel smooth, transparent, and aligned with user expectations.

Graphical interfaces excel in use cases where data visualization, structured interactions, and clear status updates are essential. Recent years have seen enormous growth in tools like Lovable, Cursor, Windsurf, and GitHub Copilot, which offer high-quality GUIs that manage context and complex multistep operations with remarkable fluidity. These tools are redefining what productive, agent-enabled interfaces look like for developers. It is time to think just as hard about what the next generation of

AI-enabled, agentic UX will be for other professions—lawyers, accountants, insurance professionals, product managers, and knowledge workers. The future of work may not revolve around documents, spreadsheets, and slide decks, but around interactive, agent-driven interfaces purpose-built for decision making, analysis, and creation.

###### **Speech and Voice Interfaces**

Speech and voice interfaces offer users a natural and hands-free way to interact with agent systems, leveraging spoken language as the primary mode of communication. From virtual assistants like Amazon’s Alexa and Apple’s Siri to customer service voice bots, these interfaces excel in scenarios where manual input is impractical or impossible—such as while driving, cooking, or operating machinery. They also provide an accessible option for users with visual impairments or limited mobility, making agent systems more inclusive.

Historically, latency has been a major barrier for speech and voice interfaces. Processing spoken language in real time—including transcribing speech, interpreting intent, and generating appropriate responses—often led to delays that disrupted conversational flow and made voice interfaces feel clunky or robotic. However, the past two years have seen astonishing advances in this space. New low-latency speech recognition models, combined with more efficient language processing architectures, have dramatically reduced delays. Equally important, the _fluidity_ and _capability_ of voice AI systems have improved, enabling more natural-sounding interactions that can handle interruptions, mid-sentence corrections, and shifts in conversation topic.

Graceful handling of interruptions is a particularly important aspect of voice interface design. Human conversations are rarely linear monologues; people interrupt themselves to clarify, change direction, or refine a request mid-sentence. Effective voice agents must mirror this conversational flexibility, allowing users to interrupt commands without confusion, revise their inputs seamlessly, and resume where they left off without forcing a complete restart. For example, a user might say, “Book me a table for—oh wait, make that tomorrow instead,” and a well-designed agent will adapt fluidly to incorporate the correction without requiring the user to start the command again. This capability not only makes interactions feel more natural but also builds trust and reduces frustration, as users feel the agent is responsive to their real communication patterns rather than demanding rigid, computer-like inputs.

Another major leap has been the integration of tool use into voice agent workflows. Modern voice agents are no longer limited to parsing commands and returning static answers. Instead, they can now pull in external context, update records, and take realtime actions—such as scheduling appointments, changing system configurations, or placing orders—based on dynamic conversational inputs. This ability to combine

natural voice interaction with structured backend operations is transforming what voice agents can achieve.

Despite these impressive technological advances, it is important to note that voice interfaces remain a frontier technology. It is true that they have entered mainstream use in smart speakers and simple assistants. However, fully conversational, multiturn, context-aware voice agents with action-taking capabilities are not yet widely deployed across industries. Many enterprises are only beginning to explore voice interfaces for customer service, healthcare, logistics, and field operations.

A key consideration in deploying voice interfaces is understanding the speed at which humans process spoken versus written information. Humans typically speak at 150– 180 words per minute, whereas reading speeds average 250–300 words per minute, with skimming speeds exceeding 500 words per minute. This means spoken interfaces are inherently slower for dense or complex information, where text-based interfaces enable faster comprehension and easier reference. However, voice excels in scenarios where hands-free convenience, natural interaction, and immediate contextual responsiveness outweigh these speed constraints.

Looking ahead, we are likely to see significant adoption of advanced voice interfaces in the coming years, driven by falling costs, reduced latency, improved speech recognition, and better orchestration with backend tools. In healthcare, voice agents can assist doctors with hands-free note-taking during patient consultations. In customer service, they are replacing rigid interactive voice response (IVR) systems with fluid, humanlike conversations that resolve issues end to end. In industrial applications, workers can control machinery, log observations, or access manuals without stopping their tasks.

Ultimately, voice interfaces are most effective for short, hands-free tasks, quick queries, and action-oriented workflows, rather than for dense information consumption or complex decision making that requires rapid skimming or side-by-side comparison.

When thoughtfully designed, speech and voice interfaces offer unparalleled convenience, accessibility, and flexibility in agent interactions. As these technologies continue to mature and integrate deeply with backend tools and knowledge systems, they are poised to become indispensable in daily workflows, personal assistants, and enterprise solutions—fundamentally transforming how users interact with AI-powered agents.

###### **Video-Based Interfaces**

Video-based interfaces are an emerging modality for agent interactions, blending visual, auditory, and sometimes textual elements into a single cohesive experience.

These interfaces can range from video avatars that simulate face-to-face conversations to agents embedded in real-time video collaboration tools. As video becomes more pervasive in our digital lives—through platforms like Zoom, Microsoft Teams, and virtual event spaces—agents are finding new ways to integrate into these environments. While many of these experiences are still in the uncanny valley, the rapid pace of improvement suggests that this technology is getting closer to prime time, and more teams will begin building experiences around it.

One of the core strengths of video interfaces is their ability to combine multiple sensory channels—visual cues, speech, text overlays, and animations—into a richer, more expressive interaction. Video agents can mimic humanlike expressions and gestures, adding emotional nuance to their communication. For example, an AIpowered customer service avatar might use facial expressions and hand gestures to reassure a frustrated customer, complementing its spoken responses with visual empathy.

However, video interfaces come with technical and design challenges. High-quality video interactions require significant processing power and bandwidth, which can introduce lag or pixelation, undermining the user experience. The uncanny valley remains a risk—if an agent’s facial expressions, gestures, or lip-syncing feel slightly off, it can create discomfort rather than engagement. Additionally, privacy concerns are amplified with video agents, as users may feel uneasy about sharing visual data with AI systems.

Looking ahead, video interfaces are poised for significant growth, especially as improvements in rendering, real-time animation, and bandwidth optimization address current limitations. In the near future, expect to see agents embedded seamlessly into virtual meetings, augmented reality (AR) overlays, and digital customer service avatars.

When thoughtfully executed, video interfaces offer an engaging, humanlike dimension to agent interactions, enhancing clarity, emotional connection, and overall effectiveness. As technology advances, video-based agents are set to play a larger role in industries such as telehealth, education, remote collaboration, and interactive entertainment, reshaping how humans and agents communicate in immersive digital spaces.

###### **Combining Modalities for Seamless Experiences**

While each interaction modality—text, graphical interfaces, voice, and video—has its own strengths and limitations, the most compelling agentic experiences often combine multiple modalities into a single, cohesive user journey. Users don’t think in terms of modality boundaries; they simply want to achieve their goals as effortlessly and naturally as possible. The ability to move seamlessly across modalities—maintaining state and context throughout—is a hallmark of great agent system design.

For example, a user might begin interacting with an agent via voice while driving, continue the conversation on their phone through text while walking into a meeting, and later review a graphical dashboard summarizing results on their laptop. In another scenario, a voice assistant might read out a summary of an analytics report before emailing a detailed, text-based version with accompanying charts for later reference. This fluid transition between modalities preserves user context, respects situational constraints, and delivers the right interaction style at each moment.

Designing for modality fluidity requires careful state management and context persistence so that information, task progress, and user preferences are never lost in transition. Agents must also adapt their communication style to suit each modality—for example, delivering concise spoken summaries while providing more detailed textual outputs for review.

This is an exciting time for the field of human-computer interaction. Recent advances in foundation models, multimodal architectures, and agent orchestration are unlocking entirely new ways of interacting with intelligent systems. For the first time, it is technically feasible to build agents that engage users across text, voice, images, and video in a single, unified workflow.

However, while the technology frontier is expanding rapidly, it is critical to remember that core UX and product principles remain unchanged. Building successful agent experiences isn’t about showcasing the latest modality integrations or generative UI capabilities for their own sake. It is about understanding users deeply, meeting them where they are, and creating intuitive, trustworthy, and delightful experiences that solve real problems in their lives.

The best products are not those that merely demonstrate technological sophistication, but those that use technology to amplify human capability in elegant and unobtrusive ways. As we continue to push the boundaries of modality design, let us stay grounded in the timeless goal of great product design: creating tools that people love to use, that make their lives easier, and that empower them to achieve what matters most.

###### **The Autonomy Slider**

A critical yet often overlooked dimension in UX design is the level of autonomy granted to agents. As Andrej Karpathy described, effective agentic systems should allow users to smoothly adjust an agent’s autonomy—from fully manual control to partial automation to fully autonomous operation. This concept, often called an autonomy slider, empowers users to choose how much control they wish to retain versus delegate at any given time.

Different users, tasks, and contexts demand different degrees of agent autonomy. In some situations, users prefer full manual control to ensure precision, while in others, they may want to offload routine or complex tasks entirely to the agent. Critically, these preferences are not static; they evolve with user trust, task familiarity, stakes, and workload. For example:

###### _Manual_

The developer writes all code themselves without agent assistance. The IDE acts purely as an editor with syntax highlighting and linting but no AI-driven suggestions.

###### _Ask (assisted)_

The agent proactively suggests code completions, refactors, or documentation snippets, but the developer reviews and accepts each suggestion before it is applied. This mode speeds up development while keeping the human fully in control.

###### _Agent_

The agent autonomously performs certain tasks, such as applying standard refactors, fixing linter errors, or generating boilerplate code files based on project conventions without requiring individual approvals. The developer is notified of changes but does not need to approve each action.

These three modes demonstrate how an autonomy slider empowers developers to balance control and efficiency within a single interface. The same principle applies beyond software development. For example, in a customer support platform:

###### _Manual_

Human agents handle all incoming customer queries themselves. The AI is inactive or used only for backend analytics, not frontline interactions.

###### _Ask (assisted)_

The agent drafts suggested replies to customer messages, surfacing recommended responses, policy references, or troubleshooting steps. The human agent

reviews, edits if necessary, and approves the reply before sending. This accelerates response time while maintaining human judgment.

###### _Agent_

The agent autonomously handles routine queries—such as password resets, order tracking, or FAQs—without human intervention, escalating only complex or sensitive issues to human agents. Users are notified of agent actions but do not need to approve each message for standard interactions.

These three modes coexist within the same customer support system, empowering teams to adjust autonomy based on query complexity, customer profile, and organizational trust in AI. This same autonomy slider pattern can extend to any field where workflows benefit from fluidly shifting between manual execution, AI assistance, and full agentic automation. This spectrum of autonomy must be consciously designed into agent experiences. Without it, agents risk feeling either underpowered (if they require too much manual input) or overbearing (if they act without user consent in sensitive contexts). To integrate an autonomy slider effectively, consider the following design principles:

###### _Expose degrees of autonomy clearly_

Users should understand the available levels of agent independence, from manual to assisted to autonomous. Label these modes in intuitive language, such as “Manual,” “Assist,” and “Auto,” and explain their implications.

###### _Enable seamless transitions_

Users must be able to shift between autonomy levels effortlessly as their confidence, context, or workload changes. For instance, a toggle or slider in the interface should offer a quick transition from review mode to auto-approve mode.

###### _Provide predictable and transparent behavior at each level_

Each autonomy level should have well-defined behaviors. In partial automation, for example, the agent may draft an output but require explicit user approval before execution. In full autonomy, it should still provide status updates and options to intervene.

###### _Communicate the risks and benefits of each level_

Users should be aware of what they gain or risk by increasing agent autonomy. For critical tasks, it may be advisable to require an explicit user confirmation before enabling full autonomy.

###### _Adapt autonomy based on user trust and competence_

Intelligent systems can gradually suggest higher autonomy levels as users gain trust and as the agent demonstrates reliability. For example, after 10 successful uses in manual mode, the system might suggest trying assist mode to save time.

Importantly, the autonomy slider is not merely a feature—it is a trust-building mechanism. By giving users control over how much autonomy an agent exercises, systems communicate respect for user expertise and agency. It avoids the common pitfall of “one-size-fits-all” autonomy that either overwhelms or underutilizes user potential. Always ask: how easily can my users move between manual, assisted, and fully autonomous modes? The answer to this question will shape whether your agent is adopted as a reliable partner or sidelined as an untrusted tool.

###### **Synchronous Versus Asynchronous Agent Experiences**

Agent systems can operate in synchronous or asynchronous modes, each offering distinct advantages and challenges. In synchronous experiences, interactions occur in real time, with immediate back-and-forth exchanges between the user and the agent. These experiences are common in chat interfaces, voice conversations, and real-time collaboration tools, where quick responses are essential for maintaining flow and engagement. In contrast, asynchronous experiences enable agents and users to operate independently, with communication occurring intermittently over time. Examples include email-like interactions, task notifications, or agent-generated reports delivered after a process has completed.

The choice between synchronous and asynchronous designs depends heavily on the nature of the task, user expectations, and operational context. While synchronous agents excel in tasks requiring instant feedback or live decision making, asynchronous agents are better suited for workflows where tasks may take longer, require background processing, or don’t demand the user’s constant attention. Striking the right balance between these modes—and managing when agents proactively engage users—can greatly influence user satisfaction and the overall effectiveness of the system. Both are useful and valid patterns, but it is highly recommended to choose which experiences fall into which category, so that users do not end up waiting for a pinwheel to spin.

###### **Design Principles for Synchronous Experiences**

Synchronous agent experiences thrive on immediacy, clarity, and responsiveness. Users expect agents in these settings to respond quickly and maintain conversation flow and context without noticeable delays. Whether in a live chat, voice call, or realtime data dashboard, synchronous interactions demand low latency and context awareness to avoid frustrating pauses or repetitive questions.

Agents in synchronous environments should prioritize clarity and brevity in their responses. Long-winded explanations or overly complex outputs can break the rhythm of real-time interactions. Additionally, turn-taking mechanics—knowing when to respond, when to wait, and when to escalate—are critical for maintaining a

natural and productive conversation flow. Visual cues, like typing indicators or progress spinners, can reassure users that the agent is actively processing their input.

Error handling is equally important in synchronous designs. Agents must gracefully recover from misunderstandings or failures without derailing the interaction. When uncertainty arises, synchronous agents should ask clarifying questions or gently redirect users rather than making risky assumptions. These principles create a smooth, intuitive experience that keeps users engaged and maintains context without unnecessary friction.

###### **Design Principles for Asynchronous Experiences**

Asynchronous agent experiences prioritize flexibility, persistence, and clarity over time. These interactions often occur in contexts where immediate responses aren’t necessary, such as when agents are processing long-running tasks, preparing detailed reports, or monitoring background events.

Effective asynchronous agents must excel at clear communication of task status and outcomes. Users should always understand what the agent is doing, what stage a task is in, and when they can expect an update. Notifications, summaries, and wellstructured reports become key tools for maintaining transparency. For example, an agent generating an analytical report might notify the user when processing begins, provide an estimated completion time, and deliver a concise, actionable summary when finished.

Context management is another critical design principle for both asynchronous and synchronous agents. Because there may be long delays between user-agent interactions, agents must retain and reference historical context seamlessly. Users shouldn’t need to repeat information or retrace previous steps when returning to an ongoing task. We’ll cover this in more detail in Chapter 6 on memory.

Lastly, asynchronous agents must manage user expectations effectively. Clear timelines, progress indicators, and follow-up notifications prevent frustration caused by uncertainty or lack of visibility into an agent’s work.

###### **Finding the Balance Between Proactive and Intrusive Agent Behavior**

One of the most delicate aspects of agent design—whether synchronous or asynchronous—is determining when and how agents should proactively engage users. Proactivity can be immensely helpful, such as when an agent alerts a user to an urgent issue, suggests an optimization, or provides a timely reminder. However, poorly timed notifications or intrusive behaviors can frustrate users, disrupt their workflow, or even cause them to disengage entirely.

The key to balancing proactivity lies in context awareness and user control. Agents should understand the user’s current focus, level of urgency, and communication

preferences. For instance, a proactive alert during a high-stakes video meeting might be more disruptive than helpful, while a notification about a completed task delivered via email might be perfectly appropriate.

Agents should also prioritize relevance when proactively reaching out. Notifications and suggestions must add genuine value—solving problems or providing insights rather than adding noise. Additionally, users should have control over notification frequency, channels, and escalation thresholds, enabling them to customize agent behavior to suit their needs.

Striking this balance isn’t just about technical capability—it’s about empathy for the user’s workflow and mental state. Well-designed agents seamlessly weave proactive engagement into their interactions, enhancing productivity and reducing friction without becoming overbearing.

###### **Context Retention and Continuity**

Ensuring context retention and continuity across user interactions is an important aspect of designing effective agent systems. Whether an agent is guiding a user through a multistep workflow, continuing a paused conversation, or adjusting its behavior based on past interactions, its ability to maintain context directly impacts usability, efficiency, and user trust.

While context retention is a technical capability, it is fundamentally a UX consideration because it determines whether users experience the agent as a cohesive, attentive collaborator or as a disconnected tool that forces them to repeat themselves. From the user’s perspective, memory creates a sense of continuity, personalization, and intelligence. If an agent remembers previous interactions, user preferences, or in-progress tasks, it can seamlessly continue conversations and workflows, reducing cognitive load and frustration.

Implementation approaches directly shape UX. A purely client-side context (e.g., stored in browser memory) may feel fast within a session but loses continuity across devices or logins, undermining seamless UX. A purely server-side context (e.g., stored in a database tied to user ID) enables long-term memory and cross-device experiences but can introduce latency or privacy considerations. A hybrid approach —maintaining short-term context on the client side for responsiveness and persisting long-term context on the server side for continuity—often achieves the best UX balance. Choosing the right strategy depends on the user journey, privacy requirements, and level of personalization intended. Ultimately, context is UX: it is how an agent remembers, adapts, and responds in ways that make it feel human-centered and supportive rather than stateless or mechanical.

Effective context retention requires agents to manage both short-term and long-term memory effectively. Short-term memory enables an agent to hold details within an

ongoing session, such as remembering the specifics of a question or instructions given moments earlier. Long-term memory, on the other hand, enables agents to retain preferences, past interactions, and broader user patterns across multiple sessions, enabling them to adapt over time.

However, context management introduces challenges. Data persistence, privacy concerns, and memory limitations must all be carefully addressed. If an agent loses track of context mid-task, the user experience can feel disjointed, repetitive, and frustrating. Conversely, if an agent retains too much context or stores unnecessary details, it risks becoming unwieldy or even breaching user privacy.

In the next section, we’ll explore two key facets of context retention and continuity: maintaining state across interactions, and personalization and adaptability—both essential for delivering fluid, intuitive, and user-centric agent experiences.

###### **Maintaining State Across Interactions**

State management is the foundation of context continuity in agent systems. For an interaction to feel seamless, an agent must accurately track what has happened so far, what the user intends to achieve, and what the next logical step is. This is particularly important in multiturn conversations, task handoffs, and workflows with intermediate states, where losing context can result in frustration, inefficiency, and abandonment of tasks.

Effective state management depends on how the system identifies and tracks users or sessions. For logged-in users, state can be tied directly to their user accounts, enabling memory persistence across devices and sessions. For anonymous interactions, maintaining context typically requires a session identifier—such as a cookie or token—to track the conversation between the client and server.

As agent systems scale to thousands or millions of users, session state should not reside only in memory. Persisting state in a database or distributed cache ensures continuity across server restarts, enables load balancing, and supports multidevice experiences. The choice between user-based memory (persistent, personalized) and session-based memory (ephemeral, session-scoped) depends on your application’s privacy requirements, user expectations, and operational architecture. Regardless of implementation, robust identification and storage strategies are fundamental to delivering seamless, context-aware agent experiences at scale.

Agents can maintain state through short-term session memory, where details of the ongoing interaction—such as a user’s recent commands or incomplete tasks—are temporarily stored until the session ends. In more advanced systems, persistent state management enables agents to resume tasks across multiple sessions so that users can pick up where they left off, even after hours or days have passed.

Effective state retention requires clear session boundaries, data validation, and fallback mechanisms. If an agent forgets context, it should gracefully recover by asking clarifying questions rather than making incorrect assumptions. Additionally, state data must be managed securely and responsibly, especially when it involves sensitive or personally identifiable information.

When done well, maintaining state enables agents to guide users through complex tasks without unnecessary repetition, reduce cognitive load, and create a sense of ongoing collaboration. Whether an agent is helping a user book travel accommodations, troubleshoot a technical issue, or manage a multistep approval process, effective state management ensures interactions remain smooth, logical, and productive.

###### **Personalization and Adaptability**

Personalization goes beyond merely remembering context—it involves using past interactions and preferences to tailor the agent’s behavior, responses, and recommendations to individual users. An adaptable agent doesn’t just maintain state; it learns from previous exchanges to deliver increasingly refined and relevant outcomes. Personalization can take multiple forms:

###### _Preference retention_

Remembering user settings, such as notification preferences or commonly chosen options

###### _Behavioral adaptation_

Adjusting response style or interaction flow based on observed user patterns

###### _Proactive assistance_

Anticipating user needs and offering suggestions based on past behavior

For example, an agent assisting with project management might recognize a user’s preferred task-tracking style and adapt its notifications or summaries accordingly. Similarly, a customer service agent might adjust its tone and verbosity based on whether the user prefers concise answers or detailed explanations.

However, personalization comes with challenges. Privacy concerns must be carefully managed, with transparent communication about what data is being stored and how it is being used. Additionally, agents must strike a balance between being helpfully adaptive and overly persistent—users should always have the option to reset or override personalized settings.

The best personalization feels invisible yet impactful, where the agent subtly improves the user experience without drawing attention to its adjustments. At its peak, personalization creates an experience where users feel understood and supported, as if the agent is a thoughtful collaborator rather than a mechanical tool.

###### **Communicating Agent Capabilities**

One of the most critical aspects of designing effective agent experiences is ensuring users understand what the agent can do and how to interact with it effectively. While backend agent design determines what functions an agent supports, the user experience determines whether those capabilities are discoverable, intuitive, and usable in practice. In traditional applications, discoverability is straightforward: menus, buttons, and interface elements visually communicate available actions. In agentic systems, especially those using text or voice interfaces, the absence of visible affordances often leaves users guessing what the agent can and cannot do.

Effective agent UX addresses this challenge by proactively communicating capabilities through the interface itself. For example, many chat-based agents include suggested action buttons below the input field, highlighting common or contextually relevant actions such as “Track order,” “Generate summary,” or “Create meeting note.” These buttons serve as visual affordances, guiding users toward supported workflows without requiring them to remember specific commands or guess what is possible. Similarly, onboarding tutorials or first-use walkthroughs can introduce users to an agent’s core functions, helping them build confidence early on.

Another useful pattern is the inclusion of expandable menus or capability cards that list available functions in a structured way. In a graphical agent interface, for instance, a sidebar might contain sections for data retrieval, analysis, summarization, and workflow automation. This mirrors the menu structures that users expect in traditional apps while communicating the breadth of agent capabilities upfront. Dynamic suggestions, where the system recommends actions based on user input, also help bridge the gap between open-ended natural language and structured tool invocation. If a user begins typing “book…,” the agent might suggest “Book meeting with [name],” “Book conference room,” or “Book travel,” anticipating intent and making actions easier to execute.

In systems relying primarily on open-ended text input, agents themselves must communicate their capabilities clearly in conversation. This can include proactive introductions when a session begins, such as: “Hi, I can help you generate content, analyze data, or summarize documents. What would you like to do today?” When users request actions beyond current capabilities, the agent should not simply reject the request but provide alternatives: “I can’t process payments directly, but I can update your billing preferences or connect you with an agent who can assist.” Such responses reduce user frustration while reinforcing the agent’s utility.

While it is important to surface capabilities, it is equally critical not to overwhelm users with too many options at once. Effective designs prioritize progressive disclosure, showing core capabilities initially and revealing advanced features as users become more comfortable. Contextual relevance also plays a key role. Displaying the

most likely actions based on current user inputs, historical behavior, or workflow stage ensures the agent feels supportive rather than cluttered. Visual grouping and clear hierarchy within menus or suggested actions help users navigate available options efficiently.

These principles apply across modalities. In text-based chat interfaces, quick-reply buttons and example prompts improve clarity. In graphical dashboards, capability menus and tooltips communicate functions without crowding the interface. Voice agents must balance brevity with clarity, listing only a few high-priority options at a time to avoid cognitive overload. Generative UI systems can combine natural language and dynamically generated visual outputs to make available capabilities immediately visible and actionable.

Ultimately, communicating agent capabilities is not merely about stating what the agent can do; it is about designing an experience that empowers users to harness those capabilities confidently and efficiently. When users understand an agent’s scope and limitations, they are far more likely to engage productively, trust its outputs, and integrate it into their workflows. Thoughtful UX design turns invisible functions into visible affordances, transforming agents from opaque black boxes into transparent, collaborative digital partners.

###### **Communicating Confidence and Uncertainty**

Agents often operate in probabilistic environments, generating outputs based on statistical models rather than deterministic rules. As a result, not every response or action carries the same degree of confidence. Communicating uncertainty effectively is essential for building user trust and helping users make informed decisions.

Confidence levels can be expressed in several ways:

###### _Explicit statements_

“I’m 90% certain this is the correct answer.”

###### _Visual cues_

Icons, color-coded alerts, or confidence meters in graphical interfaces.

###### _Behavioral adjustments_

Offering suggestions rather than firm recommendations when confidence is low.

Agents must avoid appearing overly confident when uncertainty is high—users are quick to lose trust if an agent confidently delivers an incorrect or misleading response. Similarly, excessive hedging in low-stakes interactions can make an agent appear hesitant or unreliable.

Communicating confidence and uncertainty isn’t just about sharing probabilities; it’s about framing responses in a way that aligns with user expectations and the stakes of

the interaction. In critical contexts, transparency is nonnegotiable, while in lowstakes settings, confidence can be presented more casually.

###### **Asking for Guidance and Input from Users**

No agent, no matter how advanced, can perfectly interpret ambiguous, vague, or conflicting user inputs. Instead of making risky assumptions, agents must know when to ask clarifying questions or seek user guidance. This ability transforms potential errors into opportunities for collaboration.

Effective agents are designed to ask focused, helpful questions when they encounter ambiguity. For example, if a user says “Book me a ticket to Chicago,” the agent might respond with “Would you like a one-way or round-trip ticket, and do you have preferred travel dates?” Instead of defaulting to a generic response or making incorrect assumptions, the agent uses the opportunity to refine its understanding.

The way agents ask for guidance also matters. Questions should be clear, polite, and context-aware, avoiding robotic or repetitive phrasing. If the user has already answered part of the question earlier in the conversation, the agent should reference that context rather than starting from scratch.

Additionally, agents should be transparent about why they’re asking for clarification. A simple explanation, like “I need a bit more information to proceed accurately,” helps users understand the rationale behind the question.

Finally, agents should avoid asking too many questions at once—this can overwhelm users and make the interaction feel like an interrogation. Instead, they should sequence questions logically, addressing the most critical ambiguities first.

When agents confidently ask for guidance and input, they transform uncertainty into productive collaboration, empowering users to guide the agent toward successful outcomes while maintaining a sense of partnership and shared control.

###### **Failing Gracefully**

Failure is inevitable in agentic systems. Whether due to incomplete data, ambiguous user input, technical limitations, or unexpected edge cases, agents will encounter scenarios where they cannot fulfill a request or complete a task. However, how an agent handles failure is just as important as how it handles success. A well-designed agent doesn’t just fail—it fails gracefully, minimizing user frustration, preserving trust, and providing a clear path forward.

At its core, graceful failure involves acknowledging the issue transparently, offering a helpful explanation, and suggesting actionable next steps. For instance, if an agent cannot find an answer to a query, it might respond with “I couldn’t find the

information you’re looking for; would you like me to escalate this to a human representative?” instead of producing an incorrect or nonsensical response.

Agents should also be designed to anticipate common points of failure and have predefined fallback mechanisms in place. For example, if a voice-based agent struggles to understand repeated user inputs, it might switch to a text-based option or provide a clear explanation, such as: “I’m having trouble understanding your request. Could you please try rephrasing it or typing your question instead?”

In multistep tasks, state preservation is equally important when an agent encounters failure. Instead of requiring the user to restart from scratch, the agent should retain progress and allow the user to pick up where they left off once the issue is resolved. This prevents unnecessary repetition and frustration.

Another critical aspect of graceful failure is apologetic and empathetic language. When something goes wrong, the agent should acknowledge the failure in a way that feels human and considerate, avoiding cold or overly technical error messages. For example: “I’m sorry; something went wrong while processing your request. Let me try again or connect you with someone who can help.”

Additionally, agents should provide clear paths to resolution. Whether it’s offering troubleshooting steps, escalating to a human operator, or directing the user to an alternative resource, users should always know what options are available to them when the agent encounters a roadblock.

Lastly, agents must learn from their failures whenever possible. Logging failure points, analyzing recurring issues, and feeding these insights back into the development process can help reduce the frequency of similar failures in the future. Agents that improve iteratively based on their failure patterns will become increasingly resilient and reliable over time.

In summary, failing gracefully is about maintaining user trust and minimizing frustration even when things don’t go as planned. By being transparent, empathetic, and action-oriented, agents can turn failures into opportunities to strengthen their relationship with users, demonstrating reliability even in moments of imperfection.

###### **Trust in Interaction Design**

Trust is gained in drops and lost in buckets. This certainly applies to agentic systems as well. Without it, even the most advanced agent systems will struggle to gain user acceptance, regardless of their capabilities. Transparency and predictability are two of the most powerful tools for building and maintaining trust between agents and users. Users need to understand what an agent can do, why it made a particular decision, and what its limitations are. This clarity fosters confidence, reduces anxiety, and encourages productive collaboration.

Transparency begins with clear communication of agent capabilities and constraints. Users should never have to guess whether an agent can handle a task or if it is operating within its intended scope. When agents provide explanations for their actions— whether it’s how they arrived at a recommendation, why they declined a request, or how they interpreted an ambiguous instruction—they give users visibility into their reasoning. This isn’t just about building trust; it also helps users refine their instructions, improving the quality of future interactions.

Predictability complements transparency by ensuring that agents behave consistently across different scenarios. Users should be able to anticipate how an agent will respond based on prior interactions. Erratic or inconsistent behavior, even if technically correct, can quickly erode trust. For example, if an agent suggests a cautious approach in one context but appears overly confident in a nearly identical scenario, users may start to question the agent’s reliability.

However, transparency does not mean overwhelming the user with unnecessary details. Users don’t need to see every step of the agent’s reasoning process—they just need enough insight to feel confident in its actions. Striking this balance requires thoughtful interface design, using visual cues, status messages, and brief explanations to communicate what’s happening without causing cognitive overload.

When trust and transparency are prioritized, agent systems become more than just tools—they become reliable collaborators. Users feel confident delegating tasks, following agent recommendations, and relying on their outputs in both casual and highstakes scenarios. In the remainder of this section, we’ll explore two key components of trust-building: ensuring predictability and reliability in agent behavior.

Predictability and reliability are foundational to trust. Users must be able to count on agents to behave consistently, respond appropriately, and handle errors gracefully. Agents that act erratically, give conflicting outputs, or produce unexpected behavior—even if occasionally correct—can quickly undermine user confidence.

Reliability begins with consistency in agent outputs. If a user asks an agent the same question under the same conditions, they should receive the same response. In cases where variability is unavoidable (e.g., probabilistic outputs from language models), agents should clearly signal when an answer is uncertain or context-dependent.

Agents must also handle edge cases thoughtfully. For example, when they encounter incomplete data, conflicting instructions, or ambiguous user input, they should respond predictably—either by asking clarifying questions, providing a neutral fallback response, or escalating the issue appropriately.

Another critical aspect of reliability is system resilience. Agents should be designed to recover from errors, maintain state across interruptions, and prevent cascading failures. For example, if an agent loses connection to an external API, it should notify the

user, explain the issue, and offer a sensible next step rather than silently failing or producing misleading outputs.

Lastly, reliability is about setting and meeting expectations consistently. If an agent claims it can handle a specific task, it must deliver on that promise every time. Misaligned expectations—where agents overpromise and underdeliver—can cause more damage to user trust than simply admitting limitations up front.

When agents behave predictably and reliably, they become dependable digital partners, empowering users to trust their outputs, delegate tasks confidently, and rely on them for critical decisions.

###### **Conclusion**

Designing exceptional user experiences for agent systems goes far beyond technical functionality—it requires an understanding of how humans interact with technology across different modalities, contexts, and workflows. Whether through text, graphical interfaces, voice, or video, each interaction modality carries its own strengths, tradeoffs, and unique design considerations. Successful agent experiences are those where the modality aligns seamlessly with the user’s task, environment, and expectations.

Synchronous and asynchronous agent experiences present distinct design challenges, requiring thoughtful approaches to timing, responsiveness, and clarity. Synchronous interactions demand immediacy and conversational flow, while asynchronous interactions excel in persistence, transparency, and thoughtful notifications. Striking the right balance between proactive assistance and intrusive interruptions remains one of the most delicate aspects of agent design.

Exceptional agents seamlessly retain context and adapt to users, remembering critical details across interactions and adapting intelligently to user preferences. This ability not only reduces cognitive load but also fosters a sense of continuity and collaboration, transforming agents from isolated tools into reliable digital partners. Some common patterns to keep in mind:

###### _Communicate capabilities clearly_

Show users what the agent can do through onboarding, suggestions, or buttons.

###### _Combine modalities thoughtfully_

Align text, GUI, voice, or video with the task and user context.

###### _Retain context thoughtfully_

Maintain relevant conversation state without overwhelming memory or violating privacy.

###### _Handle errors gracefully_

Provide clear, polite fallbacks when the agent can’t fulfill a request.

###### _Build trust_

Be transparent about limitations, confidence, and reasoning.

Equally important is how agents communicate their capabilities, limitations, and uncertainties. Clear expectations, honest confidence signals, and thoughtful clarification questions create trust, reduce frustration, and prevent misunderstandings. Agents must also know how to fail gracefully, guiding users toward alternative solutions without leaving them stranded or confused.

Finally, building trust through predictability, transparency, and responsible design choices ensures that users can rely on agents. Trust is earned not just through success but also through how agents handle ambiguity, failure, and recovery.

As the agent landscape continues to shift and expand, designers and developers must remain agile—continually reevaluating interaction paradigms, adapting to new multimodal capabilities, and experimenting with novel UX patterns. The design patterns described here provide a robust starting point, but the future of agentic UX will be shaped by rapid innovation in modalities, context management, and human-agent collaboration. In the years ahead, agent systems will continue to evolve, becoming more deeply embedded in our personal and professional lives. The principles outlined in this chapter—focused on clarity, adaptability, transparency, and trust—provide a blueprint for creating agent experiences that are not just functional, but intuitive, engaging, and deeply aligned with human needs.

By prioritizing UX at every stage of development, we can ensure that agents become not just tools, but indispensable partners in our increasingly intelligent digital ecosystems. In Chapter 4, we’ll cover tool use, which is how we move from ordinary chatbots to systems that can do real work for users.

### **CHAPTER 4 Tool Use**

While foundation models are great at chatting for hours, tools are the building blocks that empower AI agents to retrieve additional information and context, perform tasks, and interact with the environment in meaningful ways. In the context of AI, a tool can be defined as a specific capability or a set of actions that an agent can perform to achieve a desired outcome. These tools range from simple, single-step tasks to complex, multistep operations that require advanced reasoning and problemsolving abilities. Especially if you want your agent to make actual changes, instead of just searching for and providing information, tools will be how those changes are executed.

The significance of tools in AI agents parallels the importance of competencies in human professionals. Just as a doctor needs a diverse set of tools to diagnose and treat patients, an AI agent requires a repertoire of tools to handle various tasks effectively. This chapter aims to provide a comprehensive understanding of tools in AI agents, exploring their design, development, and deployment.

AI agents, at their core, are sophisticated systems designed to interact with their environment, process information, and execute tasks autonomously. To do this efficiently, they rely on a structured set of tools. These tools are modular components that can be developed, tested, and optimized independently, then integrated to form a cohesive system capable of complex behavior.

In practical terms, a tool could be as simple as recognizing an object in an image or as complex as managing a customer support ticket from initial contact to resolution. The design and implementation of these tools are critical to the overall functionality and effectiveness of the AI agent. We’ll start with some fundamentals of LangChain, and then cover the different types of tools that can be provided to an autonomous agent, which we will cover in sequence: local tools, API-based tools, and MCP tools.

###### **LangChain Fundamentals**

Before diving deeper into tool selection and orchestration, it is helpful to understand some core LangChain concepts. At the heart of LangChain are foundation models and chat models, which process prompts and generate responses. For example, Chat OpenAI is a wrapper class that provides a simple interface to interact with OpenAI’s chat-based models like GPT-5. You initialize it with parameters such as the model name to specify which model to use:

LangChain structures interactions as messages to maintain conversational context. The two main message types are HumanMessage , which represents user inputs, and AIMessage , which represents the model’s responses:

Tools, meanwhile, are external functions that your model can call to extend its capabilities beyond text generation—for instance, calling APIs, retrieving database entries, or performing calculations. You define a tool in LangChain using the @tool decorator, which registers the function and automatically generates the schema describing its inputs and outputs:

Once you have defined your tools, you bind them to the model using .bind_tools() , which enables the model to select and invoke these tools in response to user inputs. To interact with the model, you use the .invoke() method, providing it with a list of messages representing the current conversation. If the model decides to call a tool, it will output a tool call, which you then execute by invoking the corresponding function and appending its result back into the conversation before generating the final response:

These building blocks—chat models, messages, tools, and tool invocation—form the foundation of LangChain-based systems. Understanding how they fit together will help you follow the examples in this chapter and build your own agents that can seamlessly integrate language understanding with real-world actions.

###### **Local Tools**

These tools are designed to run locally. They are often based on predefined rules and logic, tailored to specific tasks. These local tools can be easily built and modified, and are co-deployed with the agent. They can especially augment weaknesses in language models that traditional programming techniques perform better at, such as arithmetic, time-zone conversions, calendar operations, or interactions with maps. These local tools offer precision, predictability, and simplicity. As the logic is explicitly defined, local tools tend to be predictable and reliable.

The metadata—the tool’s name, description, and schema—is just as critical as its logic. The model uses that metadata to decide which tool to invoke. Therefore, the following is important:

- Choose precise, narrowly scoped names. If your name is too general, the LLM may call it when it’s not needed.

- Write clear, distinctive descriptions. Overly broad or overlapping descriptions across multiple tools guarantee confusion and poor performance.

- Define strict input/output schemas. Explicit schemas help the foundation model understand exactly when and how to use the tool, reducing misfires.

Despite these benefits, local tools have some important drawbacks:

###### _Scalability_

Designing, building, and deploying local tools can be cumbersome, timeconsuming, and challenging, and local tools are harder to share across use cases. While tools can be exposed as libraries and shared across multiple agent use cases, this can be challenging in practice and at scale.

###### _Duplication_

Every team or agent deployment that wants to use local tools will need to deploy the same library along with their agent service, and pushing changes to these tools will require coordinating deployments to each agent service that uses these tools. In practice, many teams simply reimplement the same tools independently to avoid the coordination overhead.

###### _Maintenance_

As the environment or requirements change, handcrafted tools may need frequent updates and adjustments. This ongoing maintenance can be resourceintensive and typically requires a redeployment of your agent service.

Despite these drawbacks, manually crafted tools are especially useful in addressing areas of traditional weakness for foundation models. Simple mathematical operations are a great example of this. Unit conversions, calculator operations, calendar changes, operations on dates and times, and operations over maps and graphs, for example,

are all areas where handcrafted tools can substantially improve the efficacy of agentic systems.

Let’s look at an example of registering a calculator tool. First, we define our simple calculator function:

Then, we bind the tool with the foundation model in LangChain:

This “binding” operation registers the tool. Under the hood, LangChain will now check if the foundation model response includes any requests to call a tool. Now that we’ve bound the tool, we can ask the foundation model questions, and if the tool is helpful for answering the question, the foundation model will choose the tools, select the parameters for those tools, and invoke those functions:

The model will then include this result from the tool call in the generated final response, producing a result such as:

While the effect of this is simple, the implications are profound. The foundation model is now able to execute the computer programs that we bind with it. This is a simple example, but we can bind arbitrarily useful and consequential programs to the foundation model, and we now rely on the foundation model to choose which programs to execute with which parameters. Doing so responsibly, and only binding tools that the foundation model will execute in ways that produce more good than harm, is among the paramount responsibilities of developers building agents and agentic systems.

###### **API-Based Tools**

API-based tools enable autonomous agents to interact with external services, enhancing their capabilities by accessing additional information, processing data, and executing actions that are not feasible to perform locally. These tools leverage application programming interfaces (APIs) to communicate with public or private services, providing a dynamic and scalable way to extend the functionality of an agent.

API-based tools are particularly valuable in scenarios where the agent needs to integrate with various external systems, retrieve real-time data, or perform complex computations that would be too resource-intensive to handle internally. By connecting to APIs, agents can access a vast array of services, such as weather information, stock market data, translation services, and more, enabling them to provide richer and more accurate responses to user queries. These API-based tools have multiple benefits.

By leveraging external services, these tools can dramatically expand the range of tasks an agent can perform. For instance, an agent can use a weather API to provide current weather conditions and forecasts, a financial API to fetch stock prices, or a translation API to offer multilingual support. This ability to integrate diverse external services greatly broadens the agent’s functionality, all without having to retrain a model.

Real-time data access is another major benefit of API-based tools. APIs enable agents to access the most current information from external sources, ensuring that their responses and actions are based on up-to-date data. This is particularly crucial for applications that depend on timely and accurate information, such as financial trading or emergency response systems, where decisions must be made quickly based on the latest available data.

To illustrate the implementation of API-based tools, let’s begin with enabling your agent to browse the open web for additional information. In this code snippet, we register a tool to retrieve information from Wikipedia, a step toward a full web browsing agent:

The foundation model identifies the object of interest in the query and searches Wikipedia for the term. It then uses this additional information to generate its final answer when addressing the question:

Let’s now look at a second example, for an agent that is designed to fetch and display stock market data. This process involves defining the API interaction, handling the response, and integrating the tool into the agent’s workflow. By following this approach, agents can integrate external data sources seamlessly, enhancing their overall functionality and effectiveness.

First, we define the function that interacts with the stock market API. Then, we register this function as a tool for our agent, and we can then invoke it just like the previous tools:

Similar tools can be created to search across team- or company-specific information. By providing your agent with the tools necessary to access the information it needs to handle a task, and the specific tools to operate over that information, you can significantly expand the scope and complexity of tasks that can be automated.

When designing API tools for agents, focus on reliability, security, and graceful failure. External services can go down, so agents need fallbacks or clear error messages. Secure all communications with HTTPS and strong authentication, especially for sensitive data.

Watch out for API rate limits to avoid disruptions, and ensure compliance with data privacy laws—anonymize or obfuscate user data when needed. Handle errors robustly so the agent can recover from network issues or invalid responses without breaking the user experience. When possible, consider alternatives and multiple providers for greater reliability if any given provider is degraded.

APIs empower agents with real-time data, heavy computation, and external actions they couldn’t perform alone, making them far more capable and effective.

###### **Plug-In Tools**

These tools are modular and can be integrated into the AI agent’s framework with minimal customization. They leverage existing libraries, APIs, and third-party services to extend the agent’s capabilities without extensive development effort. Plug-in tools enable rapid deployment and scaling of the agent’s functionalities. These tools are predesigned modules that can be integrated into an AI system with minimal effort, leveraging existing libraries, APIs, and third-party services. The integration of plug-in tools has become a standard offering from leading platforms such as OpenAI, Anthropic’s Claude, Google’s Gemini, and Microsoft’s Phi as well as a growing open source community. Plug-in tools provide powerful tools to expand the capabilities of AI agents without extensive custom development.

OpenAI’s plug-ins ecosystem offers powerful extensions—everything from real-time web search to specialized code generators—but they’re only available inside the ChatGPT product, not the public API. You cannot invoke Expedia, Zapier, or any first-party ChatGPT plug-in through the standard OpenAI Completions or Chat endpoints. To replicate similar behavior in your own applications, you must build custom function-calling layers (for example, via LangChain) that approximate plugin functionality.

Anthropic’s Claude, by contrast, exposes its full “tool use” capability directly through the Anthropic Messages API (and on platforms like Amazon Bedrock or Google Cloud’s Vertex AI). You simply register your custom tools (or use Anthropicprovided ones), and Claude can call them at inference time—no separate UI required. This API-first approach makes it straightforward to integrate content moderation, bias detection, or domain-specific services into any Claude-powered workflow.

Google’s Gemini models support function calling via the Vertex AI API, letting you declare tools in a FunctionCallingConfig and have Gemini invoke them as structured calls. Whether you need natural language understanding, image recognition, or database lookups, you define the functions up front and process the returned arguments in your code—no proprietary UI layer stands between your app and the model.

Microsoft’s Phi models are offered through Azure AI Foundry, where they integrate seamlessly with other Azure services—such as cognitive search, document processing, and data visualization APIs—via the same public endpoints you use for other Azure AI models. Though not branded as “plug-ins,” Phi’s tight coupling with Azure’s productivity and analytics tools delivers a similarly smooth experience: you call the model, receive structured outputs, and feed them directly into your existing Azure workflows without switching contexts.

One of the significant advantages of plug-in tools is their integration at the model execution layer. This means these tools can be added to AI models with minimal disruption to existing workflows. Developers can simply plug these modules into their AI systems, instantly enhancing their capabilities without extensive customization or development effort. This ease of integration makes plug-in tools an attractive option for rapidly deploying new functionalities in AI applications. However, this ease of use comes with certain limitations. Plug-in tools, while powerful, do not offer the same level of customizability and adaptability as custom-developed tools that can be served either locally or remotely. They are designed to be general-purpose tools that can address a broad range of tasks, but they may not be tailored to the specific needs and nuances of every application. This trade-off between ease of integration and customizability is an important consideration for developers when choosing between plug-in tools and bespoke development.

Despite the current limitations, the catalogs of plug-in tools offered by leading platforms are rapidly growing. As these catalogs expand, the breadth of capabilities available through plug-in tools will increase, providing developers with even more tools to enhance their AI agents. This growth is driven by continuous advancements in AI research and the development of new techniques and technologies. In the near future, we can expect these plug-in tool catalogs to include more specialized and advanced functionalities, catering to a wider range of applications and industries. This expansion will facilitate agent development by providing developers with readily available

tools to address complex and diverse tasks. The growing ecosystem of plug-in tools will enable AI agents to perform increasingly sophisticated functions, making them more versatile and effective in various domains.

In addition to the offerings from major platforms, there is a rapidly growing ecosystem of tools that can be incorporated into open source foundation models. This ecosystem provides a wealth of resources for developers looking to enhance their AI agents with advanced capabilities. Open source communities are actively contributing to the development of plug-in tools, creating a collaborative environment that fosters innovation and knowledge sharing. One notable example is the Hugging Face Transformers library, which offers a wide range of pretrained models and plug-in tools for natural language processing tasks. These tools can be easily integrated into open source foundation models, enabling functionalities such as text generation, sentiment analysis, and language translation. The open source nature of this library enables developers to customize and extend these tools to suit their specific needs. The flexibility of these frameworks means that developers can combine plug-in tools with custom development, creating powerful and adaptable AI systems. The open source AI community is continuously contributing new plug-in tools and enhancements, driven by the collective efforts of researchers, developers, and enthusiasts. Platforms like Glama.ai, and mcp.so aggregate large numbers of MCP servers, making them searchable and discoverable, ranging from simple utilities to complex, stateful services. These contributions enrich the ecosystem and provide valuable resources for developers looking to leverage the latest advancements in AI.

The practical applications of plug-in tools are vast and varied, spanning multiple industries and use cases. By integrating plug-in tools, developers can create AI agents that perform a wide range of tasks efficiently and effectively. In customer support, plug-in tools can enable AI agents to handle queries, provide solutions, and manage support tickets. Tools like natural language understanding and sentiment analysis can help AI agents understand customer issues and respond appropriately, improving customer satisfaction and reducing response times. In healthcare, plug-in tools can assist AI agents in tasks such as medical image analysis, patient triage, and data management. Tools that leverage computer vision can help identify abnormalities in medical images, while natural language processing tools can assist in managing patient records and extracting relevant information from medical literature, and vector search tools can offer grounding in relevant documents to address the current query. In the finance industry, plug-in tools can enhance AI agents’ abilities to analyze market trends, detect fraudulent activities, and manage financial portfolios. Tools like anomaly detection and predictive analytics can provide valuable insights and improve decision-making processes. In education, plug-in tools can support AI agents in personalized learning, automated grading, and content recommendation.

The future of plug-in tools in AI development looks promising, with continuous advancements and growing adoption across various industries. As the capabilities of

plug-in tools expand, we can expect AI agents to become even more capable and versatile. The ongoing research and development efforts by leading platforms and the open source community will drive innovation, resulting in more powerful and sophisticated tools for AI development. One important area of focus for the future is the interoperability and standardization of plug-in tools. Establishing common standards and protocols for plug-in tools will facilitate seamless integration and interoperability across different AI platforms and systems. This will enable developers to leverage plug-in tools from various sources, creating more flexible and adaptable AI solutions. Efforts are also being made to enhance the customization and adaptability of plug-in tools. Future plug-in tools may offer more configurable options, enabling developers to tailor them to specific use cases and requirements. This will bridge the gap between the ease of integration and the need for customized solutions, providing the best of both worlds.

###### **Model Context Protocol**

As the AI ecosystem matures, agents no longer live in isolated silos. They need to read documents from cloud storage, push data to business applications, call internal APIs, and coordinate with other agents. Custom integrations—where you write bespoke adapters for each data source or service—are brittle and scale poorly. Enter the Model Context Protocol (MCP): an open standard introduced by Anthropic (and since adopted by major players like OpenAI, Google DeepMind, and Microsoft) that provides a uniform, model-agnostic way to connect LLMs to external systems. Think of MCP as a “USB-C port for AI”—a single, well-defined interface that any data source or tool can expose, and any agent can consume, without specialized glue code. At its core, MCP defines two roles:

###### _MCP server_

This is a web server that exposes data or services via a standardized JSON-RPC 2.0 interface. A server can wrap anything—cloud object storage, SQL databases, enterprise customer relationship management, proprietary business logic—so long as it implements the MCP specification.

###### _MCP client_

This is any agent or LLM application that “speaks” MCP. The client sends JSONRPC requests (e.g., “List all files in this Salesforce folder,” or “Execute function ‘getCustomerBalance’ with customerId=1234”) and receives structured JSON responses. Because the protocol is uniform, an agent developer doesn’t need to know the internals of the server—only its exposed methods.

chosen, the MCP client wraps that call into a JSON-RPC payload, sends it over to the appropriate server, and awaits a response. Because both ends speak the same language, building cross-platform interoperability becomes straightforward.

Before MCP, developers wrote custom adapters for each target system—hard-coding REST calls or SDK usage directly inside their agent code. As the number of data sources grew, these bespoke integrations multiplied, resulting in brittle, error-prone code that was difficult to maintain or extend.

Despite these advantages, several security issues have been raised and are not yet fully addressed—particularly around authentication, access controls, and potential attack vectors when multiple agents share MCP endpoints. Ensuring that only authorized agents invoke specific methods, maintaining role-based access control to sensitive data, preventing malicious payload injection, and maintaining audit logs remain active areas of research and engineering. Some organizations still rely on additional network policies or proxy layers to mitigate these risks, but the core MCP specification does not yet mandate a single, standardized security solution. Nevertheless, MCP solves a critical challenge of tool reuse across multiple agents: once a service is exposed via MCP, any number of agents can discover and invoke its methods without rewriting custom adapters for each agent. This dramatically reduces development effort and encourages modular, reusable architectures.

To see MCP in action, we’ll walk through a self-contained Python example that does the following:

1. Launches a local “math” MCP server (via a subprocess)

2. Connects to a remote “weather” MCP server running on _localhost:8000/mcp_

3. Implements an asynchronous agent loop that inspects the user’s last message and decides whether to call the “math” tool (for arithmetic expressions) or the “weather” tool (for weather queries)

4. Demonstrates how the agent parses the tool’s output and returns a final assistant response

Here’s the complete Python implementation demonstrating these steps:

The "weather" entry points to an already running HTTP MCP server at _http://localhost:8000/mcp_ . The streamable_http transport allows duplex JSON-RPC communication over HTTP/WebSocket.

MCP represents a significant step forward in how we design, deploy, and maintain AI agents at scale. By defining a single, standardized JSON-RPC interface for exposing and consuming methods, MCP decouples service implementation from agent logic, enabling any number of agents to reuse the same tools without bespoke integrations. In practice, this means that as new data sources, microservices, or legacy systems emerge, developers need only implement an MCP-compliant server once—and any MCP-capable agent can discover and invoke its methods immediately.

Although security concerns like robust authentication, fine-grained access control, and payload validation remain active areas of development, the core promise of MCP —seamless interoperability and modular tool reuse—has already been realized in production systems across leading organizations. Looking ahead, we expect continued refinement of MCP’s security best practices, broader adoption of standardized method catalogs, and the growth of an ecosystem of public and private MCP endpoints. In sum, MCP solves one of the most persistent challenges in agentic system design—how to integrate diverse services quickly and reliably—while laying a foundation for ever more flexible, maintainable, and distributed AI architectures.

###### **Stateful Tools**

Stateful tools span local scripts, external APIs, and MCP‐deployed services, yet they all share a common risk: when you hand a foundation model direct power over persistent state, you also empower it to make destructive mistakes or to be exploited by bad actors. In one real-world case, an AI agent “optimized” database performance by dropping half the rows from a production table, erasing critical records in the process. Even without malice, foundation models can misinterpret a user’s intent, turning what should be a harmless query into a destructive command. This risk is especially acute for stateful tools because they interact with live data stores whose contents change over time.

To mitigate these dangers, register only narrowly scoped operations as tools instead of exposing an “execute arbitrary SQL” endpoint. For example, define a get_user_ profile(user_id) tool or an add_new_customer(record) tool, each encapsulating a single, well-tested query or procedure. Agents needing only read access should never receive rights to delete or modify data. By constraining tool capabilities at the registration layer, you sharply reduce the attack surface and limit the scope of potential errors.

If your use case absolutely demands free-form queries, you must implement rigorous sanitization and access controls. OWASP’s GenAI Security Project warns that prompt injections can slip dangerous clauses like DROP or ALTER into otherwise benign

requests, so input validation must reject any statement containing these patterns. Always bind parameters or use prepared statements to prevent SQL injection, and ensure the database account used by the agent holds only the minimum privileges needed to execute the allowed queries.

Beyond sanitization, logging every tool invocation to detect anomalous behavior and support forensic analysis is highly recommended. Coupled with real-time alerts for suspicious patterns—such as unusually large deletions or schema-altering commands —you can intervene quickly before small errors cascade into major incidents.

Ultimately, the principle of least power should guide your design: give the model only the tools it strictly requires, and guard every operation with precise boundaries and oversight. Whether your tool runs locally, calls an external API, or executes on an MCP server, the same safeguards apply—restrict capabilities, sanitize inputs, enforce least privilege, and maintain full observability. By treating stateful tools with this level of discipline, you ensure that your AI agents remain powerful collaborators rather than uncontrolled database administrators.

###### **Automated Tool Development**

Code generation is a technique where AI agents write code autonomously, significantly reducing the time and effort required to create and maintain software applications. This process involves training models on vast amounts of code data, enabling them to understand programming languages, coding patterns, and best practices.

Code generation represents a transformative leap in AI capabilities, particularly when an agent writes its own tools in real time to solve tasks or interact with new APIs. This dynamic approach enables AI agents to adapt and expand their functionality, significantly enhancing their versatility and problem-solving capacity.

###### **Foundation Models as Tool Makers**

Foundation models no longer just consume tools—they build them. By feeding an LLM your API specifications or sample inputs, you can have it generate initial wrappers, helper functions, or higher-level “atomic” operations. Let the model draft code stubs, execute them in a safe sandbox, and then critique its own output: “That endpoint returned a 400—adjust the query parameters.” Over a few rapid iterations, you end up with a suite of well-tested, narrowly scoped tools that agents can call directly, without crafting every wrapper by hand.

This approach shines when you’re wrestling with a sprawling API landscape. Instead of manually writing dozens of microservice clients, you point the model at your OpenAPI spec (or code samples) and let it spin up a first draft of each function. Human reviewers then validate and tighten the generated code before it enters your continuous integration/continuous deployment (CI/CD) pipeline, ensuring security

and correctness. As your APIs evolve, you simply rerun the same generate-and-refine loop to keep your tools in sync—saving weeks of boilerplate work and avoiding brittle, handwritten glue code.

While foundation-driven tool creation slashes development time and scales effortlessly, it still demands clear validation criteria (tests, response checks, schema enforcement) and developer oversight. The model’s natural language critiques make it easy to understand any recommended fixes, but you’re ultimately responsible for catching edge cases, guarding against security gaps, and confirming business logic alignment. When done right, this hybrid of AI creativity and human review transforms a tangled API ecosystem into a lean, agent-ready toolkit—unlocking rapid, reliable automation across your organization.

###### **Real-Time Code Generation**

Real-time code generation involves an AI agent writing and executing code as needed during its operation. This capability enables the agent to create new tools or modify existing ones to address specific tasks, making it highly adaptable. For instance, if an AI agent encounters a novel API or an unfamiliar problem, it can generate code to interface with the API or develop a solution to the problem in real time.

The process begins with the agent analyzing the task at hand and determining the necessary steps to accomplish it. Based on its understanding, the agent writes code snippets, which it then attempts to execute. If the code does not perform as expected, the agent iteratively revises it, learning from each attempt until it achieves the desired outcome. This iterative process of trial and error enables the agent to refine its tools continuously, improving its performance and expanding its capabilities autonomously.

Real-time code generation offers several compelling advantages, particularly in terms of adaptability and efficiency. The ability to generate code on-the-fly enables AI agents to quickly adapt to new tasks and environments. This adaptability is crucial for applications requiring dynamic problem-solving and flexibility, such as real-time data analysis and complex software integration tasks. By generating code in real time, AI agents can address immediate needs without waiting for human intervention, significantly speeding up processes, reducing downtime, and enhancing overall efficiency.

However, real-time code generation also presents several challenges and risks. Quality control is a major concern, as ensuring the quality and security of autonomously generated code is critical. Poor-quality code can lead to system failures, security breaches, and other significant issues. Security risks are another major challenge, as allowing AI agents to execute self-generated code introduces the potential for malicious actors to exploit this capability to inject harmful code, leading to data breaches, unauthorized access, or system damage. Implementing robust security measures and oversight is essential to mitigate these risks.

A less obvious but critical drawback is repeatability. When your agent recreates tools from scratch each time, you lose predictability—success for one invocation doesn’t guarantee success for the next. Performance can fluctuate wildly, and subtle changes in prompts or model updates can lead to entirely different code paths. This instability complicates debugging, testing, and compliance, making it hard to certify that your agent will always behave as expected.

Resource consumption is also a critical consideration, as real-time code generation and execution can be resource-intensive, requiring substantial computational power and memory, especially when naive or inefficient solutions are drafted and executed. Placing guardrails on multiple aspects of system performance can help to mitigate these risks.

###### **Tool Use Configuration**

Foundation model APIs from OpenAI, Anthropic, Gemini, and more let you explicitly control the model’s use of tools via a tool-choice parameter—shifting from flexible foundation model–driven invocation to deterministic behavior. In “auto” mode, the model decides whether to call tools based on context; this is good for general use. In contrast, “any”/“required” forces the model to invoke at least one tool, ideal when tool output is essential. Setting these parameters to “none” blocks all tool calls—useful for controlled outputs or testing environments. Some interfaces even let you pin a specific tool, ensuring predictable, repeatable flows. By choosing the appropriate mode, you decide whether to let the foundation model manage tasks flexibly or impose structure—balancing flexibility, reliability, and predictability.

Even the best agents can misstep—skipping necessary tool calls, outputting invalid JSON, or running tools that error out—so you need reliable fallback and postprocessing mechanisms in place. After every model response, inspect whether it invoked the right tools, produced valid JSON, and succeeded without runtime errors. If anything breaks, respond with a corrective flow:

- Validate first using your schema (e.g., via jsonschema or Pydantic). This catches missing fields or malformed structures. If a tool was skipped, trigger it automatically; if the JSON is invalid, prompt the model to correct it.

- Retry intelligently, using structured logic such as exponential backoff for transient failures, or regenerate only the problematic portion instead of restarting the whole exchange.

- Fall back gracefully when retries fail. Options include switching to a backup model or service, asking the user for clarification, using cached data, or returning a safe default.

- Log everything—prompts, tool calls, validation errors, retries, fallbacks—for observability, debugging, and continuous improvement.

By validating outputs, retrying strategically, and falling back gracefully—all while logging every step—you transform random failures into manageable, predictable behavior. This shift is essential for delivering robust, production-grade agents.

###### **Conclusion**

Tools enable AI agents to perform tasks, make decisions, and interact with their environment effectively. These range from simple to complex tasks requiring advanced reasoning. Handcrafted tools, manually designed by developers, offer precision but can be time-consuming to maintain. Plug-in tools, provided by platforms like OpenAI and Google’s Gemini, enable rapid integration and scalability but lack customizability.

Automated tool development, including real-time code generation, imitation learning, and reinforcement learning, allows AI agents to dynamically adapt and refine their abilities. This enhances their versatility and problem-solving capabilities, enabling continuous improvement and autonomous expansion of tools. Building and maintaining the toolkit for your agent is one of the most critical ways to give your agent the capabilities to succeed in the task at hand.

Now that we know how to build and curate a set of tools that we provide to our agent, we’ll move on to consider how we’ll enable the agent to make plans, select and parameterize tools, and put these pieces together to perform useful work. In the next chapter, we’ll discuss how we can organize a sequence of tools to perform complex tasks in a process we call orchestration.

### **CHAPTER 5 Orchestration**

Now that your agent has a set of tools that can be used, it’s time to orchestrate them to solve real tasks. Orchestration involves more than just deciding which tools to call and when—it also requires constructing the right context for each model invocation to ensure effective, grounded actions. While simple tasks may only need a single tool and minimal context, more complex workflows demand careful planning, memory retrieval, and dynamic context assembly to perform each step accurately. In this chapter, we’ll cover orchestration strategies, context engineering, tool selection, execution, and planning topologies to build agents capable of handling realistic, multistep tasks efficiently and reliably. As we can see in, orchestration is how the system utilizes the resources at its disposal to address the user query effectively.

###### **Agent Types**

Before diving into specific orchestration strategies, it’s important to understand the different types of agents you can build. Each agent type embodies a distinct approach to reasoning, planning, and action, shaping how tasks are decomposed and executed. Some agents respond instantly with preprogrammed mappings, while others iteratively reason and reflect to handle complex, open-ended goals. The choice of agent type directly influences your system’s performance, cost, and capabilities. In this section, we will explore the spectrum: from reflex agents that provide lightning-fast responses, to deep research agents that tackle multistage investigations with adaptive plans and synthesis. Understanding these archetypes will help design agents aligned with your application needs and constraints and will illuminate how orchestration patterns, tool selection, and context construction come together within each type to achieve effective, reliable outcomes.

###### **Reflex Agents**

Reflex agents implement a direct mapping from input to action without any internal reasoning trace. Simple reflex agents follow “if-condition, then-action” rules, calling the appropriate tool immediately upon detecting predefined triggers. Because they bypass intermediate thought steps, reflex agents deliver responses with minimal latency and predictable performance, making them well suited for use cases like keyword-based routing, single-step data lookups, or basic automations (e.g., “If X, call tool Y”). However, their limited expressiveness means they cannot handle tasks requiring multistep reasoning or context beyond the immediate input.

###### **ReAct Agents**

ReAct agents interleave Reasoning and Action in an iterative loop: the model generates a _thought_ , selects and invokes a tool, observes the result, and repeats as needed. This pattern enables the agent to break complex tasks into manageable steps, updating its plan based on intermediate observations:

- ZERO_SHOT_REACT_DESCRIPTION (LangChain) presents tools and instructions in a single prompt, relying on the LLM’s innate reasoning to select and call tools without example traces.

- CHAT_ZERO_SHOT_REACT_DESCRIPTION extends this by incorporating conversational history, enabling the agent to use past exchanges when deciding on its next action.

ReAct agents excel in exploratory scenarios—dynamic data analysis, multisource aggregation, or troubleshooting—where the ability to adapt midstream outweighs the additional latency and computational overhead. Their looped structure also provides

transparency (“chain of thought”) that aids debugging and auditability, though it can increase API costs and response times.

###### **Planner-Executor Agents**

Planner-executor agents split a task into two distinct phases: planning, where the model generates a multistep plan; and execution, where each planned step is carried out via tool calls. This clear separation lets the planner focus on long-horizon reasoning while executors invoke only the necessary tools, reducing redundant LLM calls. Because the plan is explicit, debugging and monitoring become straightforward—you can inspect the generated plan, track which step failed, and replan if needed. This approach has multiple advantages:

###### _Clear decomposition_

Complex tasks break down into manageable subtasks.

###### _Debuggability_

Explicit plans reveal where and why errors occur.

###### _Cost efficiency_

Smaller models or fewer LLM calls handle execution, reserving large models for planning.

###### **Query-Decomposition Agents**

Query-decomposition agents tackle a complex question by iteratively breaking it into subquestions, invoking search or other tools for each, and then synthesizing a final answer. This pattern—often called “self-ask with search”—prompts the model: “What follow-up question do I need?” → call search → “What’s the next question?” → … → “What’s the final answer?”

Example: SELF_ASK_WITH_SEARCH Ask: “Who lived longer, X or Y?” Self-ask: “What’s X’s lifespan?” → search tool Self-ask: “What’s Y’s lifespan?” → search tool Synthesize: “X lived 85 years, Y lived 90 years, so Y lived longer”

This approach excels when external knowledge retrieval is needed, ensuring each fact is grounded in tool output before composing the final response.

###### **Reflection Agents**

Reflection and metareasoning agents extend the ReAct paradigm by not only interleaving thought and action but also reviewing past steps to identify and correct mistakes before proceeding. In this approach—exemplified by the recently proposed

ReflAct framework—the agent continuously grounds its reasoning in goal-state reflections, measuring its current state against the intended outcome and adjusting its plan when misalignments arise. Reflection prompts encourage the model to critique its own chain of thought, correct logical errors, and reinforce successful strategies, effectively simulating human-style self-assessment during complex problem-solving.

This pattern shines in high-stakes workflows where early errors can cascade into costly failures—such as financial transaction orchestration, medical diagnosis support, or critical incident response. By pairing each action with a reflection step, agents detect when tool outputs deviate from expectations and can replan or roll back before committing to irreversible operations. The added metareasoning overhead does incur extra latency and compute, but for tasks where correctness and reliability outweigh speed, reflection agents offer a powerful guardrail against error propagation and help maintain alignment with overarching goals.

###### **Deep Research Agents**

Deep research agents specialize in tackling open-ended, highly complex investigations that require extensive external knowledge gathering, hypothesis testing, and synthesis—think literature reviews, scientific discovery, or strategic market analysis. They combine multiple patterns: a planner-executor phase to chart research workflows; query-decomposition to break down big questions into targeted searches; and ReAct loops to iteratively refine hypotheses based on new findings. In a typical cycle, a deep research agent will:

1. Plan the overall research agenda (e.g., identify key subtopics or data sources).

2. Decompose each subtopic into concrete queries (via SELF_ASK or similar).

3. Invoke tools—from academic search APIs to domain-specific databases—and reflect on the relevance and reliability of each result.

4. Synthesize the insights into an evolving report or set of recommendations, using LLM-driven summarization and critique at each step.

###### **Strengths**

###### _Capability_

It can handle high-complexity, multistage investigations that lean on specialized databases and cross-disciplinary sources.

###### _Adaptive_

Research direction is adjusted as new evidence emerges.

###### _Transparent_

Explicit plans and decomposition steps make it easier to audit methodology.

###### **Weaknesses**

###### _High cost_

Extensive foundation model use and multiple API calls inflate compute and token expenses.

###### _Latency_

Each layer of planning, decomposition, and reflection adds delay.

###### _Fragility_

It is reliant on quality and availability of external data sources and needs careful error handling and fallback strategies.

The best use cases are long-form, expert-level tasks—academic literature surveys, technical due diligence, competitive intelligence—where depth and rigor trump speed.

Table 5-1 offers a snapshot of today’s most common agent archetypes—each with its own trade-offs in speed, flexibility, and complexity. However, this landscape is evolving at breakneck speed. New hybrid patterns, metareasoning frameworks, and planning strategies are emerging all the time, and the classification of agent types will only grow more nuanced. Consider this list a starting point rather than a definitive taxonomy: as the field advances, you’ll see fresh approaches built on these foundations, so stay curious, experiment often, and be ready to adapt your orchestration strategies as the research and tooling continue to mature.

_Table 5-1. Common agent archetypes_

###### **Tool Selection**

Before we get to orchestration, we will start with tool selection, because it is the foundation for more advanced planning. Different approaches to tool selection offer unique advantages and considerations, meeting different requirements and

environments. We assume a set of tools have already been developed, so if you need a refresher, go back to Chapter 4.

_Table 5-2. Tool selection strategies_

###### **Standard Tool Selection**

The simplest approach is standard tool selection. In this case, the tool, its definition, and its description are provided to a foundation model, and the model is asked to select the most appropriate tool for the given context. The output from the foundation model is then compared with the toolset, and the closest one is chosen. This approach is easy to implement, and requires no additional training, embedding, or a toolset hierarchy to use. The main drawback is latency, as it requires another foundation model call, which can add seconds to the overall response time. It can also benefit from in-context learning, where few-shot examples can be provided to boost predictive accuracy for your problem without the challenge of training or fine-tuning a model.

Effective tool selection often comes down to how you describe each capability. Start by giving every tool a concise, descriptive name (e.g., calculate_sum instead of process_numbers ) and follow it with a one-sentence summary that highlights its unique purpose (e.g., “Returns the sum of two numbers”). Include an example invocation in the description—showing typical inputs and outputs—to ground the model’s understanding in concrete terms rather than abstract language. Finally, enforce input constraints by specifying types and ranges (e.g., “x and y must be integers between 0 and 1,000”), which reduces ambiguous matches and helps the foundation model rule out irrelevant tools. By iteratively testing with representative prompts and refining each description for clarity and specificity, you’ll see significant gains in selection accuracy without any extra training or infrastructure. This sounds simple enough, but as the number of tools you register with your agent grows, overlap in the tool descriptions frequently becomes a problem and a source of mistakes in tool selection. Here we define another tool that is capable of computing mathematical expressions and evaluating formulas, something foundation models tend to not be good at:

Here’s another example of a tool you might want to register with your agent to notify a particular channel when your task is completed or needs attention for a human-inthe-loop pattern:

Now that we’ve defined our tools, we bind them to the model client and allow the model to pick which tools to invoke to best address the input:

In summary, standard tool selection offers a fast, intuitive way to integrate tools into your agent system without additional infrastructure or training overhead. While it scales well for small toolsets, careful description engineering becomes essential as your tool library grows to maintain accuracy and avoid misselection. By combining thoughtful descriptions with iterative prompt testing, you can achieve robust performance using this simple yet powerful approach.

###### **Semantic Tool Selection**

Another approach, semantic tool selection, uses semantic representations to index all of the available tools and semantic search to retrieve the most relevant tools. This reduces the number of tools to choose from and then relies on the foundation model to choose the correct tool and parameters from this much smaller set. Ahead of time, each tool definition and description is embedded using an encoder-only model— such as OpenAI’s Ada model, Amazon’s Titan model, Cohere’s Embed model, ModernBERT, or others—which represents the tool name and description as a vector of numbers. This process is which shows how each tool is embedded into a vector representation for efficient retrieval based on semantic similarity to the task query.

These tools are then indexed in a lightweight vector database. At runtime, the current context is embedded using the same embedding model, a search is performed on the database, and the top tools are selected and retrieved. These tools are then passed to the foundation model, which can then choose to invoke a tool and choose the parameters. The tool is then invoked, and the response is used to compose the response for the user. This process is which shows how the system retrieves relevant tools and uses the foundation model to select and invoke the appropriate tool with its parameters to generate the final response.

This is the most common pattern and is recommended for most use cases. It’s typically faster than standard tool selection, performant, and reasonably scalable. First, the tool database is set up by embedding the tool descriptions:

Those embeddings for your tool catalog only need to be computed once, and now they’re ready to be quickly retrieved. To choose your tool, you embed your query using the same embedding model, perform a quick database lookup, choose the parameters, and invoke our tool:

###### **Hierarchical Tool Selection**

If your scenario involves a large number of tools, however, you might need to consider hierarchical tool selection. This is especially true if many of those tools are semantically similar and you are looking to improve tool selection accuracy at the price of higher latency and complexity. In this pattern, you organize your tools into groups and provide a description for each group. Your tool selection (either generative or semantic) first selects a group and then performs a secondary search only among the tools in that group. visualizes this two-stage process, showing how a query is first routed to the appropriate tool group and then refined to a single tool within that group.

While this is slower and would be expensive to parallelize, it reduces the complexity of the tool selection task into two smaller chunks, and frequently results in higher overall tool selection accuracy. Crafting and maintaining these tool groups takes time and effort, so this is not recommended unless you have a large number of tools:

###### **Tool Execution**

Parametrization is the process of defining and setting the parameters that will guide the execution of a tool in a language model. This process is crucial, as it determines how the model interprets the task and tailors its response to meet the specific requirements. Parameters are defined by the tool definition, as discussed in more detail in Chapter 4. The current state of the agent, including progress so far, is included as additional context in the prompt window, and the foundation model is instructed to fill the parameters with appropriate data types to match the expected inputs for the function call. Additional context, such as the current time or the user’s location, can be injected into the context window to provide additional guidance for functions that require this type of information. It is recommended to use a basic parser to validate that the inputs meet the basic criteria for the data types, and to instruct the foundation model to correct the pattern if it does not pass this check.

Once the parameters are set, the tool execution phase begins. Some of these tools can easily be executed locally, while others will be executed remotely by API. During execution, the model might interact with various APIs, databases, or other tools to gather information, perform calculations, or execute actions that are necessary to complete the task. The integration of external data sources and tools can significantly enhance the utility and accuracy of the agent’s outputs. Timeout and retry logic will need to be adjusted to the latency and performance requirements for the use case.

###### **Tool Topologies**

Today, the majority of chatbot systems rely on single tool execution without planning. This makes sense: it is easier to implement, and has lower latency. If your team is developing its first agent-based system, or if that is sufficient to meet the needs for your scenario, then you can stop there after the following section, “Single Tool Execution.” For many cases, however, we want our agents to be able to perform complex tasks that require multiple tools. By providing an agent with a sufficient range of tools, you can then enable your agent to flexibly arrange those tools and apply them in correct order to solve a wider variety of problems. In traditional software engineering, the designers had to implement the exact control flow and order in which steps should be taken. Now, we can implement the tools and define the tools topology in which the agent can operate, and then allow the exact composition to be designed

dynamically in response to the context and task at hand. This section considers this range of tool topologies and discusses their trade-offs.

###### **Single Tool Execution**

We’ll begin with tasks that require precisely one tool. In this case, planning consists of choosing the one tool most appropriate to address the task. Once the tool is selected, it must be correctly parameterized based on the tool definition. The tool is then executed, and its output is used as an input when composing the final response for the user, which can be. While this is a minimal definition of a plan, it is the foundation from which we will build more complex patterns.

To make this example more concrete,.

While this single tool execution pattern is simple, it forms the foundation upon which more complex multistep planning and tool orchestration strategies are built in advanced agent systems. In the next section, we’ll look at how we can execute more tools without sacrificing latency.

###### **Parallel Tool Execution**

The first increase in complexity comes with tool parallelism. In some cases, it might be worth taking multiple actions on the input. For example, imagine that you need to look up a record for a patient. If your toolset includes multiple tools that access multiple sources of data, then it will be necessary to execute multiple actions to retrieve data from each of the sources. This increases the complexity of the problem because it is unclear how many tools need to be executed. A common approach is to retrieve a maximum number of tools that might be executed—say, five—using semantic tool selection. Next, make a second call to a foundation model with each of these five tools, and ask it to select the five or fewer tools that are necessary to the problem, filtering down to the tools necessary for the task. Similarly, the foundation model can be called repeatedly with the additional context of which tools have already been selected until it chooses to add no more tools. Once selected, these tools are independently parameterized and executed. After all tools have been completed, their results are passed to the foundation model to draft a final response for the user.

This pattern of parallel tool execution enables agents to efficiently gather comprehensive information from multiple sources in a single step. By integrating these results before composing a response, the agent can provide richer, more informed outputs while minimizing overall latency.

###### **Chains**

The next increase in complexity brings us to chains. Chains refer to sequences of actions that are executed one after another, with each action depending on the successful completion of the previous one. Planning chains involves determining the

order in which actions should be performed to achieve a specific goal while ensuring that each action leads to the next without interruption. Chains are common in tasks that involve step-by-step processes or linear workflows.

By switching to LCEL, you reduce boilerplate, gain advanced execution features, and keep your chains concise and maintainable.

The planning of chains requires careful consideration of the dependencies between actions, aiming to orchestrate a coherent flow of activity toward the desired outcome. It is highly recommended that a maximum length be set to the tool chains, as errors can compound down the length of the chain. As long as the task is not expected to fan out to multiple branching subtasks, chains provide an excellent trade-off between adding planning for multiple tools with dependencies and keeping the complexity relatively low.

###### **Graphs**

For support scenarios with multiple decision points, a graph topology models complex, nonhierarchical flows far more expressively than chains or trees. Unlike linear chains or strictly branching trees, graph structures let you define both conditional edges _and_ consolidation edges, so that parallel paths can merge back into shared nodes.

Each node in a graph represents a discrete tool invocation (or logical step), while edges—including add_conditional_edges —declare the exact conditions under which the agent may transition between steps. By consolidating outputs from multiple branches into a single downstream node (e.g., summarize_response ), you can stitch together findings from separate handlers into a unified customer reply.

However, full graph execution typically incurs significantly more foundation model calls than chains—adding latency and cost—so it’s crucial to cap depth and branching factor. In addition, cycles, unreachable nodes, or conflicting state merges introduce new classes of errors that must be managed through rigorous validation and testing. The following is an example for how to implement a graph in LangGraph:

This final wiring adds consolidation edges so that, no matter which subpath was taken—whether the user needed an invoice lookup, a refund, login troubleshooting,

Graphs offer the ultimate flexibility for modeling complex, nonlinear workflows— enabling you to branch, merge, and consolidate multiple tool executions into a unified process. However, this expressiveness comes with added overhead: more LLM calls, deeper routing logic, and the potential for cycles or unreachable paths. To harness graphs effectively, always anchor your design in your specific use case’s requirements, and resist the temptation to overcomplicate.

Start with a chain if your task is strictly linear (e.g., prompt → model → parser). Chains are easy to reason about and debug. Adopt a graph only when you must both branch and later consolidate multiple streams of information (e.g., parallel analysis steps that feed a single summary).

In practice, sketch your topology on paper first: label each node with the tool or logical step, draw arrows for the allowed transitions, and highlight where branches reunite. Then implement incrementally—cap your depth and branching factor, write unit tests for each router, and leverage LangGraph’s built-in tracing to validate that every path leads to a terminal node.

Above all, keep it as simple as possible. Every additional node or edge multiplies the potential execution paths and error modes. If a simpler chain or tree meets your needs, save the graph patterns for genuinely complex scenarios. By starting simple and iterating only as your requirements demand, you’ll build robust, maintainable orchestration that scales with confidence.

###### **Context Engineering**

Context engineering is a core component of orchestration. It ensures that each step in an agent’s plan has the right information and instructions to perform effectively. While prompt engineering focuses on writing effective instructions, context engineering involves dynamically assembling all inputs—user messages, retrieved knowledge, workflow state, and system prompts—into a structured, token-efficient context window that maximizes task performance. For example, planner-executor agents depend on clean plan outputs being passed as context to executor steps, while ReAct agents require relevant tool results embedded clearly in the prompt to inform their next reasoning cycle. Context engineering thus bridges planning and execution, enabling agent workflows to remain coherent, grounded, and aligned with user goals.

At its core, context engineering involves deciding what information to include, how to structure it for maximum clarity and relevance, and how to fit it efficiently within token limits. This includes the current user input, relevant snippets retrieved from memory or external knowledge bases, summaries of prior conversations, system instructions defining the agent’s role, and any workflow state necessary for the task at hand. In simple systems, context may consist only of a system prompt and the latest user query. But as agents tackle more complex tasks—like orchestrating multistep workflows or personalizing recommendations based on past interactions—dynamic context construction becomes critical for maintaining coherence, accuracy, and utility.

For example, an agent handling ecommerce support might construct its context by combining the system prompt defining its allowed actions, the user’s current message, a retrieved summary of the order record, and any applicable policy excerpts. In more advanced systems, the context might also include summaries of prior related conversations or the results of tool invocations from earlier in the workflow. Each additional element can improve task performance, but only if included thoughtfully; irrelevant or poorly structured context risks distracting the model or exceeding token budgets without benefit.

Effective context engineering requires several core practices. First, prioritize relevance by retrieving only the most useful information from memory or knowledge bases, rather than indiscriminately appending large blocks of text. Second, maintain clarity through structured formatting or schemas such as Model Context Protocol (MCP), which pass state and retrieved knowledge to the model in a predictable, interpretable way. Third, use summarization techniques to compress longer histories into concise representations, preserving critical details without wasting tokens. Finally, ensure that context is dynamically assembled at each inference step to reflect the agent’s current objectives, workflow stage, and user input.

Context engineering sits at the intersection of memory, knowledge, and orchestration. While orchestration decides what steps to take in a workflow, context engineering ensures that each step has the right information to execute effectively. As foundation models continue to improve, the frontier of agentic system design is shifting from model architecture to the quality of context we provide. In essence, a wellengineered context unlocks the full potential of even modest models, while poor context can undermine the performance of the most advanced systems.

By mastering context engineering, developers can create agents that are not only technically powerful but also reliable, grounded, and responsive to the needs of their users and environments. In the coming years, as memory systems, retrieval architectures, and orchestration frameworks evolve, context engineering will remain the glue that binds these components into seamless, effective experiences.

###### **Conclusion**

The success of agents relies heavily on the approach to orchestration, making it important for organizations interested in building agentic systems to invest time and energy into designing the appropriate planning strategy for the use case. Here are some best practices for designing a planning system:

- Carefully consider the requirements for latency and accuracy for your system, as there is a clear trade-off between these two factors.

- Determine the typical number of actions required for your scenario’s use case. The greater this number, the more complex an approach to planning you are likely to need.

- Assess how much the plan needs to change based on the results from prior actions. If significant adaptation is necessary, consider a technique that allows for incremental plan adjustments.

- Design a representative set of test cases to evaluate different planning approaches and identify the best fit for your use case.

- Choose the simplest planning approach that will meet your use case requirements.

With an orchestration approach that will work well for your scenario, we’ll now move on to the next part of the workflow: memory. It is worth starting small with welldesigned scenarios and simpler approaches to orchestration, and to then gradually move up the scale of complexity as necessary based on the use case. In the next chapter, we will explore how memory can further enhance your agents’ capabilities—enabling them to recall knowledge, maintain context across interactions, and perform tasks with greater intelligence and personalization.

### **CHAPTER 6 Knowledge and Memory**

Now that your agent has tools and orchestration, it is more than capable of taking actions to do real work. In most cases, though, you will want your agents to both remember what’s happened and know additional information beyond what lives in the model’s weights. In this chapter, we’ll focus on knowledge and memory—two complementary but distinct ways to enrich your agent’s context. Knowledge (often implemented via retrieval-augmented generation) pulls in factual or domain-specific content—technical specs, policy documents, product catalogs, customer or system logs—at generation time so the agent “knows” verifiable information beyond the immediate conversation to complement the information stored in the model itself, specifically in its weights and biases. Memory, on the other hand, captures the agent’s own history: prior user exchanges, tool outputs, and state updates. It lets your agent maintain continuity across turns and sessions so that it “remembers” past interactions and uses that history to inform future decisions.

In Chapter 5, we introduced context engineering as the discipline of dynamically selecting, structuring, and assembling all inputs into the model’s context window to produce the best outcomes. Memory is a foundational enabler of context engineering: it provides the knowledge, history, and facts that can be selected and assembled into effective prompts. In other words, memory is where knowledge is stored, while context engineering is how that knowledge is leveraged to produce intelligent behavior.

This chapter will offer examples in LangGraph, a low-level orchestration framework for building stateful agentic workflows that was introduced in Chapter 1. LangGraph defines your application as a directed graph of nodes (pure functions such as foundation model calls, memory updates, or tool invocations) and edges (control-flow transitions), enabling developers to model complex, multistep processes declaratively. LangGraph treats your entire application state as a single, strongly typed Python object (often a TypedDict) that flows through the graph at runtime, keeping data

management both explicit and type-safe. Unlike DAG-only (directed acyclic graph) orchestration tools, it natively supports cycles and conditional branches, making it straightforward to implement loops, retries, and dynamic decision paths without bespoke code. It also provides built-in streaming—emitting partial outcomes as they are generated—and checkpointing, so long-running agents can persist and resume exactly where they left off.

By treating memory mechanisms (rolling context windows, keyword extraction, semantic retrieval, etc.) as first-class graph nodes, LangGraph keeps memory logic modular and testable. Edges ensure memory updates occur in the correct sequence relative to LLM calls, so your agent always has the right context injected at the right time. And because state—including memory contents—can be checkpointed and resumed, your agents maintain continuity across sessions and withstand failures, all within the same unified graph framework.

In this chapter, we will first cover the fundamentals of memory for agentic systems, from simple rolling context windows to semantic memory, retrieval-augmented generation, and advanced knowledge graph approaches. Throughout, we will emphasize how these memory systems integrate into context engineering pipelines to build agents that are grounded, capable, and aligned with your specific goals and environment.

###### **Foundational Approaches to Memory**

We begin by discussing the simplest approaches to memory: relying on a rolling context window for the foundation model, and keyword-based memory. Despite their simplicity, they are more than sufficient for a wide range of use cases.

###### **Managing Context Windows**

We start with the simplest approach to memory: relying on the context window. The “context window” refers to the information that is passed to the foundation model as an input in a single call. The maximum number of tokens a foundational model can ingest and attend to in a single call is called the “context length.” This context is effectively the working memory for that request. One token averages about ¾ of a word or roughly four characters; for example, 1,000 tokens correspond to about 750 English words. Many popular models today have stepped through roughly 4,000-token (≈3,000 words, ~12 pages) and 8,000-token (≈6,000 words, ~24 pages) limits. GPT-5 and Claude 3.7 Sonnet now offer a maximum number of 272,000 tokens in their input, while Gemini 2.5 accepts up to a million tokens in the input.

The context window is a critical resource for developers to use effectively. We want to provide the foundation model with all the information it needs to complete the task, but no more. The context window is all of the information that is provided to the

foundation model when the model is called. In the simplest approach, the context window contains the current question and all previous interactions in the current session. When that window fills up, only the most recent interactions are included. In some circumstances, we will have more information to provide than we can fit into the context window. When this happens, we need to be careful with how we allocate our limited budget of tokens.

For simple use cases, you can use a rolling context window. In this case, as the interaction with the foundation model progresses, the full interaction is passed into the context window. At a certain point, the context window fills up, and the oldest parts of the context are ejected and replaced with the most recent context, in a first-in, first-out fashion. This is easy to implement, low in complexity, and will work for many use cases. The primary drawback to this approach is information will be lost, regardless of how relevant or important it is, as soon as enough interaction has occurred to eject it from the current context. With large prompts or verbose foundation model responses, this can happen quickly. Foundation models can also miss important information in large prompts, so highlighting the most relevant context and placing it close to the end of the prompt can increase the likelihood that it will be used. This standard approach to memory can be incorporated into our LangGraph agent as follows:

###### **Traditional Full-Text Search**

Traditional full-text search forms the backbone of many large-scale retrieval systems and offers a robust, mature approach to injecting precise historical context into agents enabled with foundation models. At its heart lies an inverted index, which preprocesses all text via tokenization, normalization (lowercasing, stemming), and

stop-word removal, then maps each term to the list of message chunks or documents in which it appears. This structure enables lightning-fast lookups—rather than scanning every stored message, the agent simply follows the term’s postings list to retrieve exactly those passages containing the query keywords.

To rank these results by relevance, most systems employ the BM25 scoring function. BM25 weights each passage by its term frequency (how often the query term appears), inverse document frequency (how rare the term is across the corpus), and document length normalization (penalizing overly long or overly short chunks). When a user query arrives, it is analyzed with the same text pipeline used for indexing, and BM25 produces a sorted list of the top _K_ candidate passages. These top hits —often truncated or summarized—are then injected directly into the foundation model prompt, ensuring the model sees the most pertinent historical context without exhausting its context length. Fortunately, implementing this is very easy to do in Python, though typically one would store these in a database:

In this example, we built a simple BM25-powered full-text index over our agent quips and fetched the most relevant lines for a given user query. By injecting those topranked passages directly into the prompt, we ensure the model has the key historical context—without passing every past message—and stays within its context limits.

While this keyword-driven approach excels at pinpointing exact or highly specific terms, it can miss broader themes, paraphrases, or conceptual links that weren’t expressed in the original text. To capture that deeper, “meaning-based” memory—so your agent can recall related ideas even when the exact words differ—we turn next to semantic memory and vector stores.

###### **Semantic Memory and Vector Stores**

Semantic memory, a type of long-term memory that involves the storage and retrieval of general knowledge, concepts, and past experiences, plays a critical role in enhancing the cognitive capabilities of these systems. This allows for information and past experiences to be stored and then efficiently retrieved when they are needed to improve performance later on. The leading way to do this is by using vector databases, which enable rapid indexing and retrieval at large scale, enabling agentic systems to understand and respond to queries with greater depth and relevance.

###### **Introduction to Semantic Search**

Unlike traditional keyword-based search, semantic search aims to understand the context and intent behind a query, leading to more accurate and meaningful retrieval results. At its core, semantic search focuses on the meaning of words and phrases rather than their exact match. It leverages ML techniques to interpret the context, synonyms, and relationships between words. This enables the retrieval system to comprehend the intention and deliver results that are contextually relevant, even if they don’t contain the exact search terms.

The foundation for these approaches is embeddings, which are vector representations of words that capture the words’ meanings based on their usage in large text corpora. By projecting large bodies of text into a dense numeric representation, we can create rich representations that have proven to be very useful for storage and retrieval. Popular models like Word2Vec, GloVe, and BERT have revolutionized how machines understand language by placing semantically similar words closer together in a highdimensional space. Large language models (LLMs) have further improved the performance of these embedding models across a wide range of types of text by increasing the size of the embedding model and the quantity and variety of data on which they are trained. Semantic search has proven to be an invaluable technique to improve the performance of memory within agentic systems, particularly in retrieving semantically relevant information across documents that do not share exact keywords.

###### **Implementing Semantic Memory with Vector Stores**

We begin by generating semantic embeddings for the concepts and knowledge to be stored. These embeddings are typically produced by foundation models or other natural language processing (NLP) techniques that encode textual information into dense vector representations. These vector representations, or embeddings, capture the semantic properties and relationships of data points in a continuous vector space. For example, a sentence describing a historical event can be converted into a vector that captures its semantic meaning. Once we have this vector representation, we need a place to efficiently store it. That place is a vector database, which is designed specifically to efficiently handle high-dimensional vector representations of data.

Vector stores—such as VectorDB, FAISS (Facebook AI Similarity Search), or Annoy (Approximate Nearest Neighbors Oh Yeah)—are optimized for storing and searching high-dimensional vectors. These stores are set up for fast similarity searches, enabling the retrieval of embeddings that are semantically similar to a given query.

When an agent receives a query or needs to retrieve information, it can use the vector store to perform similarity searches based on the query’s embedding. By finding and retrieving the most relevant embeddings from the vector store, the agent can access the stored semantic memory and provide informed, contextually appropriate responses. These lookups can be performed quickly, providing an efficient way to rapidly search over large volumes of information to improve the quality of actions and responses. This can be implemented as follows:

###### **Retrieval-Augmented Generation**

Incorporating memory into agentic systems not only involves storing and managing knowledge but also enhancing the system’s ability to generate contextually relevant and accurate responses. Retrieval-augmented generation (RAG) is a powerful technique that combines the strengths of retrieval-based methods and generative models to achieve this goal. By integrating retrieval mechanisms with foundation models, RAG enables agentic systems to generate more informed and contextually enriched responses, improving their performance in a wide range of applications.

First, we begin with a set of documents that might be useful to help the system answer questions. We then break these documents into smaller chunks. The idea is that the model, like a person, doesn’t need to refer to an entire long resource—it only needs the small, relevant part. We then take these chunks, embed them with an encoder model, and index them in a vector database.

During retrieval, the system searches a large corpus of documents or a vector store of embeddings to find pieces of information that are relevant to the given query or context. This phase relies on efficient retrieval mechanisms to quickly identify and extract pertinent information.

During generation, the retrieved information is then fed into a generative foundation model, which uses this context to produce a coherent and contextually appropriate response. The generative model synthesizes the retrieved data with its own learned knowledge, enhancing the relevance and accuracy of the generated text, as is.

RAG represents a powerful approach for enhancing the capabilities of agentic systems by combining retrieval-based methods with generative models. By leveraging external knowledge and integrating it into the generation process, RAG enables the creation of more informed, accurate, and contextually relevant responses. As technology continues to evolve, RAG will play a crucial role in advancing the performance and versatility of LLM-powered applications across various domains. This is especially valuable for incorporating domain- or company-specific information or policies to influence the output.

###### **Semantic Experience Memory**

While incorporating an external knowledge base with a semantic store is an effective way to incorporate external knowledge into our agent, our agent will start every session from a blank slate, and the context of long-running or complex tasks will gradually drop out of the context window. Both of these issues can be addressed by semantic experience memory.

With each user input, the text is turned into a vector representation using an embedding model. The embedding is then used as the query in a vector search across all of the previous interactions in the memory store. Part of the context window is reserved for the best matches from the semantic experience memory, then the rest of the space is allocated to the system message, latest user input, and most recent interactions. Semantic experience memory allows agentic systems to not only draw upon a broad base of knowledge but also tailor their responses and actions based on accumulated experience, leading to more adaptive and personalized behavior.

###### **GraphRAG**

We now turn to an advanced version of RAG that is more complex to incorporate into your solution but that is capable of correctly handling a wider variety of questions. Graph retrieval-augmented generation (GraphRAG) is an advanced extension of the RAG model, incorporating graph-based data structures to enhance the retrieval process. By utilizing graphs, GraphRAG can manage and utilize complex interrelationships and dependencies between pieces of information, significantly enhancing the richness and accuracy of the generated content.

Baseline RAG systems operate by chunking documents, embedding those chunks into vector space, and retrieving semantically similar chunks at query time to augment prompts for the LLM. While effective for simple fact lookup or direct questionanswering, this approach struggles when:

- Answers require connecting information scattered across multiple documents (“connecting the dots”).

- Queries involve summarizing higher-level semantic themes across a dataset.

- The dataset is large, messy, or organized narratively rather than as discrete facts.

For example, baseline RAG might fail to answer “What has Geoffrey Hinton done?” if no single retrieved chunk covers his actions comprehensively. GraphRAG addresses this by constructing a knowledge graph of entities and relationships from the dataset, enabling multihop reasoning, relationship chaining, and structured summarization.

###### **Using Knowledge Graphs**

Within a few minutes, the GraphRAG CLI can deliver global insights and local context over your texts—no Python required. But if you want more control and flexibility, production-level pipelines are just a few lines away using the neo4j graphrag python package. With the official neo4j-graphrag library, setup involves only configuring a Neo4j connection, defining an embedder, and creating a retriever—yet you immediately gain full GraphRAG capabilities. For educational or local experimentation, lightweight tools like nano graphrag or community repos (e.g.,

example-graphrag) unpack the same end to end pipeline in just a few hundred lines of Python. This system leverages the power of graph databases or knowledge graphs to store and query interconnected data. In GraphRAG, the retrieval phase doesn’t just pull relevant documents or snippets; it analyzes and retrieves nodes and edges from a graph that represents complex relationships and contexts within the data. GraphRAG consists of the following three components:

###### _Knowledge graph_

This component stores data in a graph format, where entities (nodes) and their relationships (edges) are explicitly defined. Graph databases are highly efficient at managing connected data and supporting complex queries that involve multiple hops or relationships.

###### _Retrieval system_

The retrieval system in GraphRAG is designed to query the graph database efficiently, extracting subgraphs or clusters of nodes that are most relevant to the input query or context.

###### _Generative model_

Once relevant data is retrieved in the form of a graph, the generative model synthesizes this information to create coherent and contextually rich responses.

GraphRAG represents a significant leap forward in the capabilities of agentic systems, offering sophisticated tools to handle and generate responses based on complex interconnected data. As this technology evolves, it promises to open new frontiers in AI applications, making systems smarter, more context-aware, and capable of handling increasingly complex tasks. Using knowledge graphs in GraphRAG systems transforms the way information is retrieved and utilized for generation, enabling more intelligent, contextual, and accurate responses across various applications. We will not cover the details of the algorithm here, but multiple open source implementations of GraphRAG are now available, and setting them up on your dataset is easier to do. If you have a large set of data you need to reason over, and standard chunking with a vector retrieval is running into limitations, GraphRAG is a more expensive and complex approach that frequently produces better results in practice.

###### **Building Knowledge Graphs**

Knowledge graphs are fundamental in providing structured and semantically rich information that enhances the capabilities of intelligent systems, including GraphRAG systems. Building an effective knowledge graph involves a series of steps, from data collection and processing to integration and maintenance. This section will cover the methodology for constructing knowledge graphs that can significantly impact the performance of GraphRAG systems. This process consists of several steps:

###### _1. Data collection_

The first step in building a knowledge graph is gathering the necessary data. This data can come from various sources, including databases, text documents, websites, and even user-generated content. It’s crucial to ensure the diversity and quality of sources to cover a broad spectrum of knowledge. For an organization, this may consist of a set of core policies or documents that contain core information to influence the agent.

###### _2. Data preprocessing_

Once data is collected, it needs to be cleaned and preprocessed. This step involves removing irrelevant or redundant information, correcting errors, and standardizing data formats. Preprocessing is vital for reducing noise in the data and improving the accuracy of the subsequent entity extraction process.

_3. Entity recognition and extraction_

This process involves identifying key elements (entities) from the data that will serve as nodes in the knowledge graph. Common entities include people, places, organizations, and concepts. Techniques such as named entity recognition (NER) are typically used, which may involve ML models trained on large datasets to recognize and categorize entities accurately.

_4. Relationship extraction_

After identifying entities, the next step is to determine the relationships between them. This involves parsing data to extract predicates that connect entities, forming the edges of the graph. Relationship extraction can be challenging, especially in unstructured data, though foundation models have shown improving efficacy over time.

_5. Ontology design_

An ontology defines the categories and relationships within the knowledge graph, serving as its backbone. Designing an ontology involves defining a schema that encapsulates the types of entities and the possible types of relationships between them. This schema helps in organizing the knowledge graph systematically and supports more effective querying and data retrieval.

###### _6. Graph population_

With the ontology in place, the next step is to populate the graph with the extracted entities and their relationships. This involves creating nodes and edges in the graph database according to the ontology’s structure. Databases like Neo4j, OrientDB, or Amazon Neptune can be used to manage these data structures efficiently.

###### _7. Integration and validation_

Once the graph is populated, it must be integrated with existing systems and validated to ensure accuracy and utility. This can involve linking data from other databases, resolving entity duplication (entity resolution), and verifying that the graph accurately represents the knowledge domain. Validation might involve user testing or automated checks to ensure the integrity and usability of the graph.

###### _8. Maintenance and updates_

- A knowledge graph is not a static entity; it needs regular updates and maintenance to stay relevant. This involves adding new data, updating existing information, and refining the ontology as new types of entities or relationships are identified. Automation and ML models can be instrumental in maintaining and updating the knowledge graph efficiently.

Building a knowledge graph can significantly improve complex and multihop retrieval. Typically, this is conducted by extracting semantic triples based on the Resource Description Framework data model. This consists of subject-predicateobject expressions. Foundation models are quite good at extracting these triples, so these types of knowledge graphs can now be constructed at scale. You can see this process visualized in.

To make it even more approachable, building a basic GraphRAG pipeline today is surprisingly straightforward thanks to open source tooling. Microsoft’s own GraphRAG library, available via pip install graphrag , offers a command line workflow for indexing and querying document collections—no extensive setup required. For instance, after initializing your project and indexing using their CLI, you can run:

This instantly gives you global insights and local context over your texts—without writing a single line of Python. If you prefer more control, the Neo4j GraphRAG Python package lets you set up a full GraphRAG pipeline in code. With a few lines (connecting to Neo4j, defining an embedder and retriever, then querying), you get powerful graph enhanced RAG capabilities. For developers interested in lightweight or educational implementations, there are smaller community projects like nano graphrag and example repos (e.g., example graphrag) that unpack the core pipeline in a few hundred lines of Python.

While this is great for experimentation, many teams want to move from a prototype to a hardened, scalable system. That’s where Neo4j shines: it’s the most trusted, enterprise-grade graph database available. Its native graph storage and index free adjacency architecture ensures near-constant traversal performance—even as the graph scales to billions of nodes and relationships. Production deployments often use Neo4j Enterprise or AuraDB, offering clustering, fault-tolerance, ACID (atomicity, consistency, isolation, and durability) compliance, and multiregion support. Once you’ve used the Neo4j GraphRAG Python tooling or Cypher-based setup to extract entities and define relationships, there’s a smooth path to a scalable deployment:

- Populate at scale via Cypher: use CREATE and MERGE statements to build clean, deduplicated graphs.

- Incremental loading logic ensures you can update with new data without duplication.

- Scale performance through Neo4j’s read/write clustering, cache sharding, and optimized query planner.

In short, Neo4j makes transitioning from notebook prototypes to production-grade graph-backed RAG pipelines straightforward—without sacrificing performance, reliability, or maintainability.

Once you’ve defined your ontology and extracted entities and relationships, it’s time to populate your knowledge graph. In Neo4j, this is done using the Cypher CREATE

clause, which lets you specify nodes with labels and properties and then link them via directed relationships. Best practice is to first load or match existing nodes—ensuring you don’t duplicate entities—and then issue separate CREATE statements for each relationship, as shown in the following example. By organizing your script into discrete steps (create nodes → match nodes → create relationships), you maintain clarity and can more easily debug or extend your graph as it grows:

###### **MATCH**

###### **MATCH**

###### **MATCH**

###### **MATCH**

###### **MATCH**

Once loaded, your knowledge graph supports multihop traversals (e.g., shortestPath queries) and rich relationship patterns that far exceed what a flat table or vector store can express. This foundation enables advanced GraphRAG workflows—where an agent can traverse the graph at runtime to gather context spanning several degrees of separation—unlocking truly powerful reasoning over structured knowledge. These structures make it easy to discover underlying relationships in the data. For instance, it is now possible to search for elements on the graph, then retrieve all the elements that are one or more links away from that node. As you can see in, when answering complex queries, the controller can traverse the graph and perform multihop reasoning over structured data, expanding the range and complexity of questions these types of systems can answer.

This provides an efficient way to retrieve relevant context for addressing a task. As AI technology progresses, the methodologies for building, integrating, and maintaining knowledge graphs will continue to evolve, further enhancing their utility in various domains.

###### **Promise and Peril of Dynamic Knowledge Graphs**

Dynamic knowledge graphs are a significant step forward in managing and utilizing knowledge in real-time applications. These graphs are continuously updated with new information, adapting to changes in knowledge and context, which can significantly enhance GraphRAG systems. However, the dynamic nature of these graphs also introduces specific challenges that need careful consideration. This section explores the potential benefits and risks associated with dynamic knowledge graphs.

As the developer, it is important to apply careful consideration to choose the most appropriate design to retrieve the appropriate context for handling incoming tasks efficiently. A knowledge graph is reasonably easy to prototype, but getting one ready for production is a significant undertaking.

Recent advances in model architectures are pushing context windows to unprecedented lengths, allowing LLMs to “remember” and process entire documents in a single pass. For example, Google’s Gemini 2.5 and OpenAI’s GPT-4.1 now support up to _one million_ tokens—roughly 750,000 words or over 2,500 pages—enabling retrieval-free generation of very large contexts. Similarly, index-free RAG systems embed their own retrieval logic into long-context models such as GPT-4.1, effectively performing chunking and relevance scoring internally without external vector stores or inverted indices. Embedding knowledge directly into these extended contexts can simplify pipelines: rather than orchestrating separate retrieval and ranking nodes, an agent

can load entire knowledge bases (e.g., policy manuals or technical specs) directly into the prompt and rely on the model’s attention mechanisms to surface relevant passages.

However, these retrieval-free approaches come with trade-offs. Processing millions of tokens in one shot demands substantial compute and can introduce latency and cost challenges—sometimes negating the simplicity gains of removing external retrieval. In addition, there is no guarantee that a given model will correctly identify the one piece of relevant information from such a large context window. Do not be surprised if larger models, larger context windows, and more compute make elaborate text search and semantic search over vector databases obsolete, but in the meantime, the community consensus remains that hybrid architectures retain value: even with multipage context windows, RAG can outperform pure long-context models on factseeking queries and enterprise use cases, especially when memory freshness or precision ranking is critical. In practice, many production systems combine extended context windows with selective retrieval nodes—leveraging the best of both worlds to balance performance, cost, and factual accuracy.

Dynamic real-time information processing is greatly enhanced by dynamic knowledge graphs, which can integrate real-time data. This capability is particularly useful in environments where information is constantly changing, such as news, social media, and live monitoring systems. By ensuring that the system’s responses are always based on the most current and relevant information, dynamic knowledge graphs provide a significant advantage.

Adaptive learning is another key feature of dynamic knowledge graphs. They continuously update themselves, learning from new data without the need for periodic retraining or manual updates. This adaptability is crucial for applications in fastevolving fields like medicine, technology, and finance, where staying updated with the latest knowledge is critical. This helps organizations make informed decisions quickly, which is invaluable in scenarios where decisions have significant implications and depend heavily on the latest information. Knowledge graphs also provide critical information in a structured format that can be operated effectively and reasoned over, can provide far greater flexibility than vector stores, and are especially valuable for understanding the rich context of an entity. Unfortunately, these benefits come with some important drawbacks:

###### _Complexity in maintenance_

Maintaining the accuracy and reliability of a dynamic knowledge graph is significantly more challenging than managing a static one. The continuous influx of new data can introduce errors and inconsistencies, which may propagate through the graph if not identified and corrected promptly.

###### _Resource intensity_

The processes of updating, validating, and maintaining dynamic knowledge graphs require substantial computational resources. These processes can become resource-intensive, especially as the size and complexity of the graph grow, potentially limiting scalability.

###### _Security and privacy concerns_

Dynamic knowledge graphs that incorporate user data or sensitive information must be managed with strict adherence to security and privacy standards. The real-time aspect of these graphs can complicate compliance with data protection regulations, as any oversight might lead to significant breaches.

###### _Dependency and overreliance_

There is a risk of overreliance on dynamic knowledge graphs for decision making, potentially leading to a lack of critical oversight. Decisions driven solely by automated insights from a graph might overlook external factors that the graph does not capture.

To harness the benefits of dynamic knowledge graphs while mitigating their risks, several strategies can be employed. Implementing robust validation mechanisms with automated tools and processes is essential for continuously ensuring the accuracy and reliability of data within the graph. Designing a scalable architecture using technologies such as distributed databases and cloud computing helps manage the computational demands of dynamic graphs. Strong security measures, including encryption, access controls, and anonymization techniques, are crucial to ensure that all data inputs and integrations comply with current security and privacy regulations. Additionally, maintaining human oversight in critical decision-making processes mitigates the risks of errors and overreliance on automated systems.

Dynamic knowledge graphs offer substantial promise for enhancing the intelligence and responsiveness of GraphRAG systems, providing significant benefits across various applications. However, the complexities and risks associated with their dynamic nature necessitate careful management and oversight. By addressing these challenges proactively, the potential of dynamic knowledge graphs can be fully realized, driving forward the capabilities of intelligent systems in an ever-evolving digital landscape.

###### **Note-Taking**

With this technique, the foundation model is prompted to specifically inject notes on the input context without trying to answer the question.<sup>1</sup> This mimics the way that we might fill in the margins or summarize a paragraph or section. This note-taking is performed before the question is presented, and then interleaves these notes with the original context when attempting to address the current task. Experiments show good results on multiple reasoning and evaluation tasks, with potential for adaptation to a wider range of scenarios. As we can see in, in a traditional, “vanilla” approach, the model is provided with the context and a question, and it produces an answer. With chain of thought, it has time to reason about the problem, and only subsequently generate its answer to the question. With the self-note approach, the model generates notes on multiple parts of the context, and then generates a note on the question, before finally moving to generate the final answer.

> 1 Jack Lanchantin et al., “Learning to Reason and Memorize with Self-Notes”, arXiv, May 1, 2023.

###### **Conclusion**

Memory is critical to the successful operation of agentic systems, and while the standard approach of relying on the context window of recent interactions is sufficient for many use cases, more challenging scenarios can benefit substantially from the investment into a more robust approach. We have explored several approaches here, including semantic memory, GraphRAG, and working memory.

This chapter has delved into various aspects of how memory can be structured and utilized to enhance the capabilities of intelligent agents. From the basic concepts of managing context windows, through the advanced applications of semantic memory and vector stores, to the innovative practices of dynamic knowledge graphs and working memory, we have explored a comprehensive range of techniques and technologies that play crucial roles in the development of agentic systems.

Memory systems in agentic applications are not just about storing data but about transforming how agents interact with their environment and end users. By continually improving these systems, we can create more intelligent, responsive, and capable agents that can perform a wide range of tasks more effectively. In the next chapter, we will explore how agents can learn from experience to improve automatically over time.

### **CHAPTER 7 Learning in Agentic Systems**

This chapter covers different techniques for approaching and integrating learning into agentic systems. Adding the capability for agents to learn and improve over time is an incredibly useful addition, but is not necessary when designing agents. Implementing learning capabilities takes additional design, evaluation, and monitoring, which may or may not be worth the investment depending on the application. By learning, we mean improving the performance of the agentic system through interaction with the environment. This process enables agents to adapt to changing conditions, refine their strategies, and enhance their overall effectiveness.

Nonparametric learning refers to techniques to change and improve performance automatically without changing the parameters of the models involved. In contrast, parametric learning refers to techniques in which we specifically train or fine-tune the parameters of the foundation model. We will start by exploring nonparametric learning techniques, then cover parametric fine-tuning approaches, including supervised fine-tuning and direct preference optimization, that adapt model weights for targeted improvements.

###### **Nonparametric Learning**

Multiple techniques exist to do this, and we will explore several of the most common and useful approaches.

###### **Nonparametric Exemplar Learning**

The simplest of these techniques is exemplar learning. In this approach, as the agent performs its task, it is provided with a measure of quality, and those examples are used to improve future performance. These examples are used as few-shot examples

for in-context learning. In the simplest version, fixed few-shot examples, they are hardcoded into the prompt and do not change (the left side of ).

If we have more examples, we can continue adding them into the prompt, but that eventually comes with increases in cost and latency. In addition, not all examples might be useful for all inputs. A common way to address this is to dynamically select the most relevant examples to include in the prompt (see on the right side of ). These experiences, as examples, are then stored in a way that makes them accessible for future reference. This typically involves building a memory bank where details of each interaction—such as the context, actions taken, outcomes, and any feedback received—are stored. This database acts much like human memory, where past experiences shape understanding and guide future actions. Each experience provides a data point that the agent can reference to make better decisions when encountering similar situations. This method enables agents to build a repository of knowledge that can be drawn upon to improve performance.

The agent retrieves information from its database of past cases to solve new problems. Each stored case consists of a problem description, a solution that was applied, and the outcome of that solution. When faced with a new situation, the agent searches its memory to find similar past cases, analyzes the solutions that were applied, and adapts them if necessary to fit the new circumstances. This method allows for high flexibility, as the agent can modify its approach based on what has or has not worked in the past, thus continually refining its problem-solving strategies.

When successful examples are saved in persistent storage, then retrieved and provided as examples in the prompt, performance increases significantly on a range of tasks. This is a well-established finding and has been confirmed across a variety of domains. In practice, this provides us with a simple, transparent, and lightweight way

to rapidly improve the agent performance on given tasks. As the number of successful examples increases, it then becomes wise to retrieve the most relevant successful examples by type, text retrieval, or semantic retrieval. Note that this technique can be applied to the agentic task execution as a whole, or it can be performed independently on subsets of the task.

###### **Reflexion**

Reflexion equips an agent with a simple, language-based habit of self-critique: after each unsuccessful attempt, the agent writes a brief reflection on what went wrong and how to improve its next try. Over time, these reflections live in a “memory buffer” alongside the agent’s prior actions and observations. Before each new attempt, the agent rereads its most recent reflections, allowing it to adjust its strategy without ever retraining the model.

At a high level, the Reflexion loop works like this:

1. _Perform an action sequence._ The agent interacts with the environment using its usual prompt-driven planning.

2. _Log the trial._ Every step—actions taken, observations received, success or failure—is appended to a log in persistent storage (for example, a JSON file or database table).

3. _Generate a reflection._ If the trial fails, the agent constructs a short “reflection prompt” that includes the recent interaction history plus a template asking: “What strategy did I miss? What should I do differently next time?” The LLM produces a concise plan.

4. _Update memory._ A helper function (update_memory) reads the trial logs, invokes the LLM on the reflection prompt, and then saves the new reflection back into the agent’s memory structure.

5. _Inject reflections on the next run._ When the agent attempts the same (or a similar) task again, it prepends its most recent reflections into the prompt, guiding the model toward the improved strategy.

Reflexion is very lightweight. You don’t touch model weights; you simply use the foundation model as its own coach. Reflexion accommodates both numerical feedback (e.g., a success flag) and free-form comments, and it has been shown to boost performance on tasks ranging from code debugging to multistep reasoning.

The prompt is built in three sections to turn the model into its own coach: first, a brief framing instruction tells the model “you failed your task—focus on strategic missteps rather than summarizing the environment and output your corrective plan after the word ‘Plan,’” which ensures a concise, parseable response. Next, under “Instruction:” we restate the original goal (“find a dairy-free, apple variety pack of chips under $30”), anchoring the reflection in the true objective. Finally, we include the complete Action/Observation transcript of the failed run—every search, click, and internal thought ending with STATUS: FAIL —so the model has concrete evidence of what went wrong. By ending with the cue “Plan:” we signal the model to shift from diagnosis to prescription, yielding a focused set of next-step recommendations. Here’s the Python implementation that sets up our three-part coaching prompt—framing instruction, restated goal under “Instruction:” and the full Action/Observation transcript—ending with the cue “Plan:”:

###### **Experiential Learning**

Experiential learning takes nonparametric learning a step further. In this approach, the agent still gathers its experiences into a database, but now it applies a new step of aggregating insights across those experiences to improve its future policy. This is especially valuable for reflecting on past failures and attempting to develop new techniques to improve performance in similar situations in the future. As the agent extracts insights from its experience bank, it maintains this list of insights over time, and it dynamically modifies these insights, promoting the most valuable insights, downvoting the least useful ones, and revising insights based on new experiences.

This work builds on Reflexion by adding a process for cross-task learning. This allows the agent to improve its performance when it moves across different tasks and helps identify good practices that can transfer. In this approach, ExpeL maintains a list of insights that are extracted from past experiences. Over time, new insights can be added, and existing insights can be edited, upvoted, downvoted, or removed, as can be.

This process begins with a simple effort of asking the foundation model to reflect on the observation returned from the environment, with the goal of identifying insights that can lead to better performance on the task in the future:

This may work well when we have a small number of examples to learn from, but what if we have many? This technique offers a simple but effective way to manage this: the insights generated are regularly reevaluated and adjusted in relative importance to the other rules. For example, a sample prompt to reflect on previous actions to generate new rules that improve performance on future trials could be:

By examining and contrasting to the successful trial, and the list of existing rules, you can perform the following operations: add, edit, remove, or agree so that the new list of rules is GENERAL and HIGH LEVEL critiques of the failed trial or proposed way of Thought so they can be used to avoid similar failures when encountered with different questions in the future. Have an emphasis on critiquing how to perform better Thought and Action. (ExpeL)

These learned rules are then regularly reevaluated and adjusted in importance relative to the other rules derived from experience. The methodology for evaluating and improving the existing rules is as follows:

This process is a bit more involved, but it still relies on manageable logic. Specifically, this process enables helpful insights to be dynamically improved upon in subsequent experiences. This process is in which the model is used to extract insights from pairs of successful and unsuccessful examples, and in which insights are promoted and demoted over time, distilling out a small list of insights that are used to guide and improve the performance of the agent.

In this next section, we see how these rules are actually created, promoted, modified, and removed to enable the agent to improve its performance on the task over time:

With sufficient feedback, this process provides an efficient way to learn from interactions with the environment and improve performance over time. An added advantage of this approach is its capability to facilitate the agent’s gradual adaptation to nonstationary environments. Thus, if your agent needs to adjust its policy to a changing environment, this approach enables it to do so effectively. Let’s now take a look at some example usage:

As you can see, even a small number of lines of code can enable an agent to continually learn from experience to improve performance on a specific task. These approaches are very practical, affordable, easy to implement, and enable continual adaptation from experience. In some cases, though, and especially when we have a large number of samples to learn from, it can make sense to consider fine-tuning.

###### **Parametric Learning: Fine-Tuning**

Parametric learning involves adjusting the parameters of a predefined model to improve its performance on specific tasks. When we have evaluation data, we can use it to improve the performance of our system. It often makes sense to start with nonparametric approaches, because they are simpler and faster to implement. Adding examples and insights into the prompt takes time and computational resources, though. When we have a sufficient number of examples, it might be worth considering fine-tuning your models as well to improve your agentic performance on your tasks. Fine-tuning is a common approach where a pretrained model is adapted to new tasks or datasets by making small adjustments to its parameters.

###### **Fine-Tuning Large Foundation Models**

Most developers begin building agentic systems with generic large foundation models such as GPT-5, Claude Opus, Gemini, and other similar classes of models because these offer an exceptional level of performance across a variety of tasks. These models are pretrained on extensive, general-purpose datasets, which equip them with a vast amount of linguistic and conceptual knowledge. These companies invest a great deal of effort in their own post-training processes. Fine-tuning these models involves making targeted adjustments to their parameters, tailoring them to specific tasks or domains. This process allows developers to adapt the model’s extensive knowledge to

specialized applications, boosting its relevance and effectiveness on specific tasks while retaining its general capabilities.

Deciding whether to invest in fine-tuning hinges on your specific needs, resources, and longer-term maintenance plans. Consider fine-tuning in the following scenarios:

###### _Domain specialization is critical_

You need the model to speak your organization’s jargon, follow a strict style guide, or handle highly sensitive content with minimal errors. Off-the-shelf models often struggle with narrow domains, and supervised fine-tuning (SFT) or direct preference optimization (DPO) can lock in that expertise.

###### _Consistent tone and format matter_

If every response must adhere to a precise template—say, financial disclosures or legal disclaimers—fine-tuning ensures the model reliably produces the correct structure without elaborate prompt engineering.

###### _Tool and API calls must be precise_

When your agent regularly invokes external functions or services (e.g., medical dosages, trading APIs), function-calling fine-tuning can drastically reduce miscalls and handle edge-case errors more gracefully than in-context prompts alone.

###### _You have sufficient high-quality data and budget_

Fine-tuning large models demands hundreds to thousands of curated examples, expert graders (for reinforcement fine-tuning [RFT]), and GPU hours. If you lack data or compute, nonparametric methods like Reflexion or exemplar retrieval may offer better ROI.

###### _Retraining frequency is manageable_

Fine-tuned models require version management, retraining schedules, and compatibility checks. If your domain changes frequently, the upkeep cost can outweigh the performance gains.

When to hold off:

###### _You’re in rapid prototyping or low-volume use_

Early in development, nonparametric learning or prompt engineering lets you iterate at zero retraining cost. Only commit to fine-tuning once your use case and data pipelines are stable.

###### _Model evolution could invalidate your effort_

Proprietary LLM providers regularly release improved base models. A new GPT-5 update may outperform your fine-tuned GPT-4, wiping out months of retraining work. Always weigh your fine-tuning investment against the pace of upstream model advances.

###### _You’re experiencing resource constraints_

If GPU availability is limited, annotation is expensive, or inference speed is a priority, consider nonparametric strategies like retrieval-augmented generation. They can deliver many of the same benefits at a fraction of the cost and with far lower initial investment and ongoing maintenance.

In short, fine-tune a model only when your performance requirements, data availability, and operational capacity align—and always maintain a clear plan for retraining or migrating when the next generation of base models arrives. It’s important to note that pretraining—training a model from scratch on trillions of tokens—is an undertaking reserved for major AI labs with vast compute resources and proprietary data. For nearly all teams, the best approach is to start with high-quality open source models that have appropriate licenses for your use case. Often, these models already include post-training or instruction tuning that aligns closely with your task needs. In many cases, this eliminates the need for additional fine-tuning altogether, or at least reduces it to minimal targeted updates. Before investing in fine-tuning, always explore whether an existing pretrained or instruction-tuned model can meet your requirements with prompt engineering, nonparametric learning, or lightweight adaptation techniques. When in doubt, don’t fine-tune your model. There are often lowercost, higher-leverage activities you can take to improve your product. Table 7-1 shows the primary methods for fine-tuning language models.

_Table 7-1. Primary methods for fine-tuning language models_

Fine-tuning offers four distinct levers for adapting pretrained models to your needs:

###### _Supervised fine-tuning (SFT)_

SFT uses curated (prompt, response) pairs to teach the model exactly how it should behave, making it ideal for classification tasks, structured outputs, or correcting instruction-following errors.

###### _Vision fine-tuning_

Vision fine-tuning injects labeled image-label pairs to sharpen a model’s multimodal understanding—perfect when you need robust image classification or more reliable handling of visual inputs.

###### _Direct preference optimization (DPO)_

DPO trains the model on paired “good versus bad” responses, helping it learn to favor higher-quality outputs, which is especially useful for tuning tone, style, or summarization priorities.

###### _Reinforcement fine-tuning (RFT)_

RFT leverages expert-graded outputs and policy-gradient updates to reinforce complex reasoning chains, making it the go-to for high-stakes domains like legal analysis or medical decision support.

Large foundation models excel at absorbing vast amounts of general knowledge, but their true power emerges when you fine-tune them on domain-specific data. A GPT-5 model customized for financial documents, for example, will not only parse jargon correctly but also adhere to your organization’s precise reporting conventions. Similarly, a legal-tuned model can surface case law insights with the right tone of voice, while a customer-support tune can ensure every reply follows your corporate guidelines. This tight alignment between the model’s internal representations and your real-world context is why fine-tuning remains indispensable for mission-critical applications.

That said, fine-tuning large models demands serious resources. Billions of parameters translate into heavy GPU requirements, lengthy training runs, and nontrivial cloud costs. Retraining to keep up with evolving data or to correct drift can multiply these expenses, and real-time deployments may suffer from higher inference latency as a result. For organizations without dedicated ML infrastructure, these barriers can make large-model fine-tuning impractical.

Equally important is the need for high-quality, task-specific training data. Large models only become “better” in your domain when they see enough representative examples—often in the thousands—to internalize subtle patterns. Curating, labeling, and validating these datasets is time-consuming and can introduce bias if not handled carefully. Without rigorous data governance and robust hold-out testing, you risk overfitting your model to stale or unrepresentative examples, limiting its ability to generalize and retain fairness.

Despite these challenges, fine-tuning large models remains a powerful approach, especially in cases where high performance is critical and the resources to support such models are available. The unparalleled capacity of large models enables them to perform at exceptional levels when fine-tuned for specific tasks, often surpassing the performance of smaller, task-specific models. This makes them ideal for applications where accuracy, depth of understanding, and nuanced language handling are necessary, such as healthcare diagnostics, legal analysis, or complex technical support.

Fine-tuning language models is a large and complex domain, encompassing a wide range of techniques, architectures, and trade-offs. In this section, we are not attempting to cover every nuance or training approach in depth. Instead, the examples provided here are intended as an introduction to the topic—offering practical illustrations to help you assess whether fine-tuning might be worth deeper investment for your own projects. If you find that these methods align with your goals, there are many excellent resources, papers, and open source toolkits available to continue your learning journey into fine-tuning strategies, scalable optimization, and production deployment.

Large foundation models offer a powerful solution for applications requiring high accuracy, adaptability, and nuanced understanding. Fine-tuning these models enables

developers to harness their extensive pretrained knowledge while optimizing performance for specialized tasks or domains. While the computational and data requirements are significant, the benefits of fine-tuning large models can justify the investment for applications demanding peak performance and robust language comprehension, but it is only recommended for a small number of use cases.

###### **The Promise of Small Models**

In contrast to large foundation models, small models offer a more resource-efficient alternative, making them suitable for many applications where computational resources are limited or response time is critical. While small models inherently have fewer parameters and simpler architectures, they can still be surprisingly effective when finely tuned to a specific task. This adaptability stems from their simplicity, which not only allows for faster adaptation but also enables rapid experimentation with different training configurations. Small models are particularly advantageous in environments where deploying larger, more complex models would be costly, impractical, or excessive given the task requirements.

The lean architecture of small models offers unique advantages in transparency and interpretability. Because they have fewer layers and parameters, it is easier to analyze their decision-making processes and to understand the factors influencing their outputs. This interpretability is invaluable in applications where explainability is essential—such as finance, healthcare, and regulatory domains—as stakeholders need clear insights into how and why decisions are made. For instance, a small model fine-tuned for medical image classification can be more straightforward to debug and validate, providing assurance to medical practitioners who rely on its predictions. In these contexts, smaller models contribute to increased accountability and trust, particularly in high-stakes applications where the reasoning behind decisions must be understandable and accessible.

Small models also enable Agile development workflows. Their lightweight structure allows for faster iterations during fine-tuning, which can lead to quicker insights and adjustments. For developers working in Agile environments or with limited access to high-performance computing, small models provide a flexible, responsive solution. They are ideal for tasks requiring continuous or incremental learning, where models must be frequently updated with new data to maintain relevance. Moreover, small models can be deployed effectively in real-time systems, such as embedded devices, mobile applications, or Internet of Things networks, where low latency is essential. In these applications, the reduced computational footprint of small models enables efficient processing without compromising the overall system’s responsiveness.

Another key advantage of small models is their accessibility, both in terms of cost and availability. Many high-performing small models are open source and freely available, including models like Llama and Phi, which can be modified to suit various use cases.

This accessibility lowers barriers for organizations and developers who may not have the budget or infrastructure to support large-scale models. Small models allow these teams to experiment, innovate, and deploy ML solutions without incurring significant operational costs. This democratization of ML technology enables more organizations to harness the benefits of AI, contributing to a more inclusive development ecosystem.

In terms of performance, fine-tuned small models can achieve results comparable to those of larger models on specific, narrowly defined tasks. For example, a small model fine-tuned for sentiment analysis within a particular domain, such as financial reports, can achieve high accuracy because it specializes in recognizing patterns specific to that context. When applied to well-defined tasks with clear data boundaries, small models can match, or even surpass, the performance of larger models by focusing all of their capacity on the relevant aspects of the task. This efficiency is particularly valuable in applications with high accuracy demands but limited data, where small models can be customized to perform effectively without overfitting.

In addition to their efficiency, small models support a sustainable approach to AI development. Training and deploying large models consume significant energy and computational resources, which contribute to environmental impacts. Small models, however, require substantially less energy for training and inference, making them a more sustainable choice for applications where resource consumption is a concern. Organizations prioritizing environmental sustainability can integrate small models as part of their green AI strategies, contributing to reduced carbon footprints without compromising on innovation.

The promise of small models extends to settings where frequent updates or retraining are needed. In scenarios where the data landscape changes rapidly—such as social media sentiment analysis, real-time fraud detection, or personalized recommendations—small models can be quickly retrained or fine-tuned with new data, adapting rapidly to changing patterns. This ability to frequently update without high retraining costs makes small models ideal for applications where adaptability is crucial. Additionally, small models can be deployed in federated learning environments, where data privacy concerns require models to be trained across decentralized data sources. In these settings, small models can be efficiently fine-tuned on edge devices, enabling privacy-preserving AI solutions.

Fine-tuning smaller models represents a rapidly evolving landscape—a kaleidoscope of architectures, sizes, and capabilities that can deliver near-state-of-the-art performance at a fraction of the compute and cost. In early 2025, benchmarks like Stanford’s HELM (Holistic Evaluation of Language Models) showcased open weight models such as DeepSeek-v3 and Llama 3.1 Instruct Turbo (70B) achieving mean scores above 66% on MMLU, and even 8B-parameter variants like Gemini 2.0 FlashLite began to crack the 64% threshold. In addition, Baytech Consulting reported that

Phi-3-mini (3.8B) matched 540B-parameter PaLM’s 60% MMLU score, a 142× size reduction in two years. Mobile-MMLU further highlighted that models under 9B can excel on edge-focused tasks, although variance grows as parameter counts fall.

This pace means that the “best” small model family today—be it Llama 3 (8B–70B), Qwen2.5 Turbo (72B), or the emerging Palmyra and DeepSeek lines—may be eclipsed within months. To stay current, practitioners should rely on trusted thirdparty leaderboards:

- Stanford HELM publishes live MMLU, GPQA, and IFEval scores across dozens of models.

- Papers With Code aggregates benchmarks and provides downloadable artifacts for comparative analysis.

- Hugging Face’s Evaluation on the Hub offers an API to fetch up-to-date results on common tasks like GSM8K and HumanEval.

- BigBench Leaderboard tracks performance on the BBH suite, complementing HELM’s broader scope.

When choosing a small model, consider your deployment constraints—latency, hardware, budget—and task demands. Models with fewer than eight billion parameters are unbeatable for on-device or low-cost inference; 8B–70B families strike a sweet spot for general reasoning; above that, proprietary giants like GPT-5 still lead in highstakes accuracy. By combining these resources with periodic leaderboard checks, you can navigate this shifting terrain and select the optimal small-model family for your agentic application—while acknowledging that the field’s rapid churn will likely deposit a new champion by the time you finish reading this chapter.

###### **Supervised Fine-Tuning**

Among parametric approaches, supervised fine-tuning remains the foundational technique, enabling precise behavioral shaping through curated input/output examples. SFT is the foundational approach for precisely steering an agent’s behavior by showing it explicit examples of how to respond. One powerful use case is teaching an agent exactly when and how to invoke external APIs—fine-tuning function calling so the agent not only formats tool calls correctly but also reasons whether a call should happen at all. This extends what standard hosted function calling offers, providing more control and consistency when prompt engineering alone falls short. While offthe-shelf foundation models continue to improve at generating function calls, you may encounter stubborn cases where your prompts grow unwieldy, parameters are repeatedly mis-parsed, or accuracy lags behind your domain’s strict requirements. In those scenarios—especially if you’re driving high-volume traffic and every percentage point of reliability matters—fine-tuning on curated examples can both boost performance and, over time, reduce your per call costs compared with token-

expensive proprietary endpoints. In essence, SFT uses carefully curated (prompt, response) pairs to help the model learn the desired output style, structure, or behavior. The same technique can adapt an agent for consistent tone, structured output, or —in this example—precise tool use. You can see this process.

To make function calls robust, you’ll typically define an explicit schema for each API you expose—specifying function names, valid arguments, types, and return formats. This ensures your examples teach the agent the _contract_ it must follow. To do this, you assemble a fine-tuning dataset of structured examples that mirror your exact API schema—function names, argument types, and return formats—so the model internalizes your toolset’s contract. The result is a model that not only formats calls correctly on the first try, but also makes contextual judgments about whether a function should be invoked at all. Because this approach demands extra data curation, compute resources, and maintenance, we recommend starting with the pretrained models’ built-in function-calling and runtime schema validation. Only once you’ve confirmed that prompt engineering and standard APIs fall short, should you consider this more heavyweight investment—ideally when your scale and precision requirements justify the up-front effort.

This involves presenting the model with structured examples where the agent must choose whether to make a function call, populate arguments accurately, and wrap the result appropriately. For example, if a user asks, “What’s the weather in Boston?”, a well-tuned agent should call a get_weather(location="Boston") function, and then incorporate the result into its reply. But if the user says, “Imagine it’s snowing in Boston—what should I wear?”, the agent should reason hypothetically without triggering a real call. This type of contextual judgment is learned through targeted examples.

To ensure your fine-tuned agent generates only well-formed, safe function invocations, it’s critical to define and enforce a clear schema for every API or tool you expose. By codifying each function’s name, argument types, and return structure in a machine-readable format—such as JSON Schema or a TypeScript/Zod schema—you give the model a precise contract to follow. During fine-tuning, include these schemas alongside your examples so the model learns not just what to call but exactly how to structure its JSON payload. At runtime, validate every proposed call against the same schema (using libraries like Zod, Ajv, or Pydantic) before executing it; any mismatch can be caught early and either corrected or rejected, preventing malformed or malicious requests. This end-to-end schema discipline drastically reduces errors, simplifies debugging, and hardens your system against unexpected inputs.

Fine-tuning also helps the model learn how to parse user inputs into valid arguments, recover from errors (like missing parameters), and gracefully fall back if the function call fails. Special tokens and formatting—such as wrapping the agent’s internal reasoning in <think>…</think> or enclosing a call in <tool_call>…</tool_call> —can help the model distinguish between dialogue, thought, and action.

The following is a minimal working pattern for the supervised fine-tuning of a language model with LoRA (Low-Rank Adaptation) adapters for function calling. This includes preprocessing conversations into a consistent _chat template_ :

1. Attaching special tokens for <think> or <tool_call> segments

2. Using LoRA to adapt only targeted layers efficiently

3. Training with SFTTrainer to update the model on your dataset of correct (prompt, response) pairs

We start with the preprocess function, which structures the data appropriately for training:

Here, we wrap the model’s internal reasoning and external tool calls in special tokens, like <think>…</think> and <tool_call>…</tool_call> . This makes it easy for the model to separate its “thoughts” from its API actions:

Each example is tokenized and added to a training dataset, and then fine-tuned using standard supervised learning techniques with LoRA for efficiency. The training loop uses SFTTrainer from Hugging Face’s TRL library, which supports features like sequence packing and gradient checkpointing:

When agents depend on reliable tool use—retrieving calendar entries, executing commands, or querying databases—SFT makes these calls dramatically more robust than prompt engineering alone. It lowers error rates, teaches contextual judgment (when _not_ to call), and reduces your token cost by cutting retries and malformed calls.

It also introduces a layer of reasoning: the model can choose when not to call a tool. For example, if the user says “If it rains tomorrow, I’ll stay in,” the agent can reason that no API call is needed and simply reply.

Finally, this method improves user experience by enabling agents to handle complex tasks with reliability. As agents take on more responsibility—especially in automation and decision-making roles—structured function calling becomes a foundational skill worth fine-tuning.

###### **Direct Preference Optimization**

Building on SFT, direct preference optimization introduces preference learning, aligning outputs more closely with human-ranked quality judgments. DPO is a finetuning technique that trains a model to prefer better outputs over worse ones by learning from ranked pairs. Unlike standard SFT, which simply teaches the model to replicate a “gold” output, DPO helps the model internalize preference judgments— improving its ability to rank and select high-quality completions at inference time.

The following is a minimal working example using a small Phi-3 model to fine-tune help desk response quality:

Next, we load our dataset containing ranked pairs. Each example includes a prompt, a preferred (“chosen”) response, and a less preferred (“rejected”) response. This structure enables the model to learn which outputs to favor during training:

With our data prepared, we define training hyperparameters and configure DPO. The beta parameter adjusts how strongly the model prioritizes the preferred response during optimization:

In summary, this script loads a base Phi-3 model with LoRA adapters, prepares a dataset of preference-ranked examples, and fine-tunes the model using DPOTrainer . After training, the model can produce higher-quality outputs that reflect your defined preferences more reliably than standard SFT alone.

DPO is especially useful when your primary goal is to shape output _quality_ rather than simply replicate examples. It complements SFT by adding a preference-learning dimension, helping your agents produce outputs that are not only correct but also aligned with nuanced human expectations.

###### **Reinforcement Learning with Verifiable Rewards**

Building on preference-based fine-tuning, reinforcement learning with verifiable rewards (RLVR) introduces policy optimization against an explicit, measurable reward function.

Unlike preference-based approaches, RLVR enables you to connect any grader you can build—automated metrics, rule-based validators, external scoring models, or human evaluators—and directly optimize your model toward those rewards. This unlocks scalable, targeted improvement for virtually any task where you can define a verifiable evaluation signal. Whether optimizing summarization quality, correctness of tool calls, factuality of knowledge retrieval, or even adherence to safety constraints, RLVR transforms static preference learning into a general, extensible reinforcement learning framework.

Unlike DPO, which directly optimizes for pairwise preferences, RLVR combines preference learning with reinforcement learning, enabling the model to generalize beyond observed rankings by predicting value scores and optimizing its outputs accordingly.

In the interest of readability, we will not include the full code for RLVR here, but it can be found in the accompanying repository for those who wish to implement it in practice.

Benefits of RLVR include its flexibility to optimize against any measurable signal, its ability to generalize beyond observed examples through value prediction, and its suitability for tasks where automated grading or scalable human evaluation is available. RLVR is particularly effective when you have ranked preference data or when you can build a reliable scoring function to evaluate outputs. It is ideal for scenarios requiring continual quality improvement, especially when rewards are sparse or evaluation is too costly to obtain at scale through direct human labeling alone.

In summary, RLVR expands the possibilities of RFT by combining preference learning with value-based policy optimization. This allows your models not just to imitate preferred outputs, but to predict and optimize for what will be most useful, accurate, or aligned—paving the way for self-improving, task-specialized foundation models.

###### **Conclusion**

Learning in agentic systems encompasses a variety of approaches, each offering distinct advantages for improving performance and adaptability. Nonparametric learning enables agents to learn dynamically from experience without modifying underlying model parameters, emphasizing simplicity, speed, and real-world responsiveness. Parametric learning, by contrast, directly fine-tunes model weights to achieve deeper specialization—whether through supervised fine-tuning for structured outputs and function calling, or through direct preference optimization to shape output quality according to nuanced human judgments. Together, these learning methods form a powerful toolkit. By combining nonparametric agility with targeted parametric adaptation, developers can create intelligent, robust agents capable of evolving alongside changing tasks and environments—while ensuring each investment in learning aligns with operational constraints and performance goals.

### **CHAPTER 8 From One Agent to Many**

Most use cases start with one agent, but as the number of tools increases, and the range of problems you want your agent to solve increases, introducing a multiagent pattern can improve the overall performance and reliability. Just as we saw that it’s probably not a good idea to put all of your code in a single file, or bundle all of your backend servers into a single monolith, many of the lessons we learned about the principles of software architecture and service design still apply when building systems with AI and foundation models. As you continue to add functionality and capabilities into your agentic system, you’ll soon find the need to break up your system into smaller agents that can be independently validated, tested, integrated, and reused. In this chapter, we’ll discuss how and when to add an agent to your system, and how to organize and manage them.

###### **How Many Agents Do I Need?**

Begin with a simple approach, and only add complexity as needed to improve performance. The appropriate number and organization of agents will vary enormously based on the difficulty of the tasks, the number of tools, and the complexity of the environment.

###### **Single-Agent Scenarios**

We’ll begin with single-agent systems, which are suitable for tasks that are of modest difficulty, a limited number of tools, and lower-complexity environments. They are also often better when latency is critical, as multiagent systems typically require multiple exchanges between agents, which increases the latency for the user. As a result, it is typically best practice to begin with a single-agent system, as it is often faster and cheaper than extending to multiagent systems. In this approach, a single agent is responsible for invoking tools, if available, up to a limit before responding to the user.

In this, the agent performs tasks and chooses when to invoke tools or submit the answer. The primary benefits include:

###### _Simplicity_

Easier implementation and management

###### _Lower resource requirements_

Less computational overhead

###### _Latency_

Quicker response for users

Single-agent systems offer a strong starting point for building agentic applications. Their simplicity, lower cost, and reduced latency make them well suited for many practical scenarios—especially when the task scope is limited and performance requirements are tight. While they may not scale well to highly complex or multifaceted tasks, starting with a single-agent architecture enables teams to validate core functionality quickly and iterate efficiently. Only when the complexity, toolset, or task coordination needs outgrow the capacity of a single agent should developers consider transitioning to more sophisticated multiagent systems.

To illustrate, consider a single-agent system for supply chain logistics management. This agent handles a broad set of tools for inventory, shipping, and supplier tasks in one unified prompt and graph. While effective for basic queries, performance can degrade with too many tools, as the agent must select from a large set. Here’s how we set up a single agent with 16 tools:

However, as the toolset expands—here, to 16—the agent’s system prompt must describe all possibilities, potentially leading to confusion or suboptimal choices. This is where the single-agent model’s limitations begin to show, paving the way for

multiagent decomposition. Now, let’s complete the agent setup with the foundation model binding, state definition, and graph construction:

With the agent fully assembled, we see the elegance of a single-node LangGraph: the state holds operation details and messages, the model call analyzes queries and invokes tools, and the graph is minimal—just one “assistant” node. This structure minimizes overhead, ensuring low latency as there’s no inter-agent communication. In practice, as demonstrated in 2025 LangGraph tutorials for supply chain agents, such setups can process queries in under a second on standard hardware, making them ideal for operational dashboards or real-time alerts.

For most use cases, though, the key bottleneck arises when the number of tools and responsibilities increases. When an agent is expected to choose the correct tool from a set, performance degrades as the potential number of tools increases. Before jumping to multiagents, consider scaling within the single-agent framework: for instance, encapsulate multiple tools into larger groupings (e.g., via hierarchical tool selection), or use semantic tool selection using a vector database as described in Chapter 5 on orchestration. If these approaches still fall short, decomposing tools into distinct agents with appropriate responsibilities can then improve reliability and performance, though it introduces coordination overhead.

###### **Multiagent Scenarios**

In multiagent systems, multiple agents collaborate to achieve shared goals, an approach that is especially advantageous when tasks are complex and require varied toolsets, parallel processing, or adaptability to dynamic environments. A key benefit of multiagent systems is specialization: each agent can be assigned specific roles or areas of expertise, allowing the system to leverage each agent’s strengths effectively. This division of labor enables agents to focus on defined aspects of a task, which improves efficiency and ensures that specialized tools are applied where they are most needed. By distributing tools and responsibilities across agents, multiagent systems address the limitations faced by single-agent systems, especially when tasks require expertise across different domains or when the number of tools required exceeds what a single agent can manage reliably.

Building on the single-agent supply chain example from the previous subsection, let’s evolve it into a multiagent system. Here, we decompose the 16 tools into three specialized agents: one for inventory and warehouse management, one for transportation and logistics, and one for supplier relations and compliance. A supervisor agent routes queries to the appropriate specialist, embodying manager coordination (detailed in “Manager Coordination” on page 181). This setup demonstrates specialization by narrowing each agent’s toolset and prompt, reducing selection errors and improving reliability. The code begins with imports and a shared response tool, ensuring all specialists can communicate outcomes uniformly. This shared tool minimizes duplication while allowing decentralized execution:

With tools grouped, we bind them to separate language model instances for each specialist. This allows for tailored prompts and reduces context size per agent, enhancing focus and efficiency. Multiagent architectures like this enable parallel processing (e.g., one agent optimizing delivery while another evaluates suppliers) cutting response times in high-volume logistics. The shared state ensures seamless handoffs.

The supervisor node acts as a central coordinator, analyzing queries and routing to specialists—exemplifying streamlined decision making without full consensus overhead. Specialist nodes then process independently, invoking tools and responding. This structure mitigates conflicts through clear role boundaries and enables parallelism if edges are expanded to concurrent calls:

Finally, the graph assembles the system with conditional edges for routing, enabling adaptability as the supervisor dynamically selects based on query content. In execution, this enables efficient handling of diverse tasks without a single point of overload. While coordination adds some latency, the benefits in scalability and reliability far outweigh it for complex environments:

This multiagent framework exemplifies the power of adaptability in action. For instance, if a query involves a sudden supply disruption during peak season, the supervisor could route it to the transportation specialist for immediate containment, while the inventory specialist concurrently scales warehouse operations. This type of dynamic rerouting has become commonplace, enabling systems to pivot in response to real-time data like weather events or market shifts, thereby minimizing downtime and optimizing resource allocation. In our code, the conditional edges facilitate this flexibility, as the supervisor’s output determines the flow, enabling the system to handle evolving conditions without rigid predefined paths. This not only boosts throughput through potential parallelism—such as forking to multiple specialists if extended —but also enhances resilience, as failures in one agent (e.g., due to API downtime) don’t halt the entire process.

Adaptability is another core advantage, as multiagent systems can respond dynamically to changing conditions. By coordinating their actions, agents can reallocate roles and responsibilities as needed, adapting to new information or environmental changes in real time. This adaptability enables the system to remain efficient and effective in complex and unpredictable scenarios, where static, single-agent approaches may struggle to keep up.

However, multiagent systems are not without challenges. With multiple agents interacting, the complexity of coordination increases, requiring sophisticated communication and synchronization mechanisms to ensure agents work harmoniously. Communication overhead is another challenge, as agents must frequently exchange information to stay aligned and avoid duplicating efforts. This need for communication can slow down the system and introduce additional resource demands, especially in large-scale applications. Additionally, conflicts between agents may arise if they pursue overlapping goals or fail to prioritize effectively, necessitating protocols for conflict resolution and resource allocation.

In sum, while multiagent systems offer powerful advantages in handling complex, multifaceted tasks, they also require careful planning to manage the additional complexity and coordination requirements they introduce. By assigning agents distinct roles, enabling parallel processing, and incorporating adaptability and redundancy, multiagent systems can achieve high levels of performance, reliability, and flexibility, particularly in scenarios where a single-agent approach would fall short.

###### **Swarms**

Swarms represent a distinctive approach to agentic system design, inspired by decentralized systems in nature—such as flocks of birds, schools of fish, or colonies of ants. In swarm-based systems, large numbers of simple agents operate with minimal individual intelligence but collectively give rise to intelligent, emergent behavior through local interactions and simple rules.

Unlike traditional multiagent systems, which often rely on explicit role assignment and centralized coordination, swarm systems emphasize decentralization and selforganization. Each agent follows its own set of local policies or behaviors, typically without a global view of the system. Yet, through repeated, local interactions—such as broadcasting small updates, reacting to neighbors, or adapting based on shared signals—the swarm can adapt to changing conditions, solve complex problems, and exhibit robust group-level behavior. Key advantages of swarm-based systems include:

###### _Scalability_

Because swarm agents are loosely coupled and locally driven, the system can scale to hundreds or thousands of agents with minimal coordination overhead.

###### _Robustness_

There is no single point of failure. If individual agents fail, others can continue operating without significant degradation in performance.

###### _Flexibility_

Swarms can adapt in real time to changing goals or environments, making them well suited to dynamic or unpredictable scenarios.

###### _Distributed problem-solving_

Tasks such as exploration, monitoring, consensus formation, or distributed search can be tackled effectively through swarm dynamics.

Swarms are particularly effective in environments where centralized control is impractical or undesirable. For example, they are useful in large-scale data discovery, researching across multiple sources, or distributed decision making. In these scenarios, agents can operate semi-independently, contribute small insights or actions, and let global behavior emerge from the accumulation of local actions.

However, designing swarm systems comes with unique challenges, especially around predictability, observability, and efficiency. Despite these limitations, swarm-based systems offer a powerful and elegant solution for problems that benefit from decentralization, parallelism, and resilience. While not suitable for every problem domain, swarms shine in distributed environments and are increasingly relevant in fields like edge computing, sensor networks, and real-time collaborative systems—especially where flexibility and robustness matter more than precision or central control.

###### **Principles for Adding Agents**

When expanding a system by adding more agents, a strategic approach is essential to ensure the system remains efficient, manageable, and effective. The following principles serve as guidelines for optimizing agent-based design and functionality:

###### _Task decomposition_

Task decomposition is a foundational principle, emphasizing the importance of breaking down complex tasks into smaller, manageable subtasks. By decomposing tasks, each agent can focus on a specific aspect of the workload, simplifying its responsibilities and improving efficiency. Clear task boundaries reduce overlap and redundancy, ensuring that each agent’s contribution is valuable and that no effort is wasted. This decomposition not only enhances individual agent performance but also makes the system easier to coordinate and scale.

###### _Specialization_

Specialization enables agents to be assigned roles that match their strengths, thereby maximizing the system’s collective capabilities. When each agent is tasked with activities that align with its specific functions, the system operates with greater precision and effectiveness. Specialized agents are more adept at handling particular types of work, which translates to improved performance and faster task execution overall. By designing agents with distinct responsibilities, the system can leverage diverse expertise to address complex or multidisciplinary tasks.

###### _Parsimony_

Parsimony is a guiding principle that encourages adding only the minimal number of agents necessary to achieve the desired functionality and performance. This principle emphasizes simplicity and efficiency, reminding developers that each agent added to the system introduces additional communication overhead, coordination complexity, and resource demands. By adhering to parsimony, developers avoid unnecessary agent proliferation, which can lead to increased maintenance burdens and potential performance bottlenecks. Parsimony requires careful assessment of each agent’s role and a disciplined approach to agent allocation, ensuring that each addition provides clear value to the system. Before adding an agent, developers should consider whether its responsibilities could be fulfilled by existing agents or by enhancing current capabilities. This focus on simplicity results in a streamlined, more manageable system that performs effectively without excessive redundancy. Ultimately, parsimony promotes an efficient, lean multiagent system that maximizes functionality while minimizing the risks and costs associated with complexity.

###### _Coordination_

Coordination is critical for the harmonious operation of multiagent systems. To maintain alignment among agents, robust communication protocols must be established, facilitating efficient information sharing and reducing the risk of conflicts. Coordination mechanisms should also include protocols for conflict resolution, particularly when agents have overlapping tasks or resource requirements. When agents can exchange information seamlessly and resolve issues

autonomously, the system is more resilient and adaptable, capable of responding efficiently to dynamic scenarios.

###### _Robustness_

Robustness is essential for enhancing fault tolerance and resilience. Redundancy involves adding agents that can take over if others fail, providing backup support that ensures uninterrupted operation. In high-stakes environments, redundancy is invaluable for maintaining system stability and reliability. Robustness also encompasses designing agents and workflows that can withstand unexpected disruptions, such as network failures or agent downtime. By embedding redundancy and robustness into the system, developers can ensure that it remains functional even in adverse conditions.

###### _Efficiency_

Efficiency helps in assessing the trade-offs between adding agents and the potential complexity or resource demands that come with them. Each additional agent increases computational requirements and coordination overhead, so it is crucial to weigh the advantages of expanded functionality against these costs. By carefully evaluating the costs and benefits of each agent addition, developers can make informed decisions that balance system performance, resource efficiency, and scalability.

By following these principles, developers can determine the optimal number and configuration of agents required to achieve the desired balance of performance, efficiency, and complexity. This thoughtful approach enables the creation of multiagent systems that are both capable and sustainable, maximizing the benefits of additional agents while minimizing potential downsides.

###### **Multiagent Coordination**

Effective coordination among agents is critical for the success of multiagent systems. Various coordination strategies can be employed, each with its advantages and challenges. This section explores several of the leading coordination strategies, but we may see new approaches emerge.

###### **Democratic Coordination**

In democratic coordination, each agent within the system is given equal decisionmaking power, with the goal of reaching consensus on actions and solutions. This approach is characterized by decentralized control, where no single agent is designated as the leader. Instead, agents collaborate and share information equally, contributing their unique perspectives to collectively arrive at a decision. The key strength of democratic coordination is its robustness; because no agent holds a dominant role, the system has no single point of failure. This means that even if one or more agents

experience failures, the overall system can continue functioning effectively. Another advantage is flexibility: when agents collaborate openly, they can quickly adapt to changes in their environment by updating their collective input. This adaptability is essential in dynamic settings where responsiveness to new information is crucial.

Moreover, democratic coordination promotes equity among agents, ensuring that all participants have an equal voice, which can lead to fairer outcomes.

However, democratic coordination comes with its own set of challenges. The process of reaching a consensus often requires extensive communication between agents, leading to significant communication overhead. As each agent must contribute and negotiate their perspective, the decision-making process can also be slow, potentially causing delays in environments where quick responses are necessary. Furthermore, implementing a democratic coordination protocol is often complex, as it requires well-defined communication and conflict-resolution mechanisms to facilitate consensus building. Despite these challenges, democratic coordination is particularly well suited for applications that prioritize fairness and robustness, such as distributed sensor networks or collaborative robotics, where each agent’s contribution is valuable and consensus is essential for system success.

###### **Manager Coordination**

Manager coordination adopts a more centralized approach, where one or more agents are designated as managers that are responsible for overseeing and directing the actions of subordinate agents. In this model, managers take on a supervisory role, making decisions, distributing tasks, and resolving conflicts among agents under their guidance. One of the primary advantages of manager coordination is its streamlined decision making. Because managers have the authority to make decisions on behalf of the group, the system can operate more efficiently, bypassing the lengthy negotiation process required in democratic systems. This centralization also enables managers to clearly assign tasks and responsibilities, ensuring that agents focus on specific objectives without duplicating efforts or causing conflicts. Additionally, manager coordination simplifies communication pathways, as subordinate agents primarily communicate with their designated manager rather than with every other agent, reducing coordination complexity.

However, the reliance on managers introduces certain vulnerabilities. A single point of failure exists because if a manager agent fails or is compromised, the entire system may experience disruptions. Additionally, scalability becomes a concern as the system grows; managers can become bottlenecks if they cannot handle the increased volume of tasks or interactions required in larger networks. Finally, the centralized nature of decision making in manager coordination can reduce adaptability, as managers may not always be able to make the most informed decisions based on real-time changes within each subordinate’s environment. This type of coordination is particularly

effective in structured, hierarchical settings like manufacturing systems or customer support centers, where centralized control allows for optimized workflows and quicker conflict resolution.

###### **Hierarchical Coordination**

Hierarchical coordination takes a multitiered approach to organization, combining elements of both centralized and decentralized control through a structured hierarchy. In this system, agents are organized into multiple levels, with higher-level agents overseeing and directing those below them while affording subordinate agents a degree of autonomy. This approach provides significant scalability benefits, as the hierarchical structure enables coordination responsibilities to be distributed across multiple levels. By doing so, the system can manage a large number of agents more efficiently than a fully centralized model. The layered design also introduces redundancy, as tasks can be managed at different levels, improving fault tolerance. Clear lines of authority within the hierarchy streamline operations, with higher-level agents handling strategic decisions and lower-level agents focusing on tactical execution.

Despite these advantages, hierarchical coordination presents its own challenges. The complexity of designing a hierarchical system can be substantial, as each level must be carefully structured to ensure smooth coordination between layers. Communication delays can arise due to the need for information to propagate through multiple levels before reaching all agents, which can slow down responsiveness to urgent changes. Additionally, decision making at higher levels may introduce latency, as lower-level agents may need to wait for instructions before acting. Despite these challenges, hierarchical coordination is well suited for large, complex systems such as supply chain management or military operations, where different levels of coordination can handle both high-level planning and on-the-ground execution.

###### **Actor-Critic Approaches**

The actor-critic pattern in agentic systems is a lightweight form of evaluation-driven iteration. In this setup, the actor is responsible for generating candidate outputs— such as answers, plans, or actions—while the critic serves as a quality gate, accepting or rejecting outputs based on a predefined rubric.

The process is simple: the actor keeps producing candidates until the critic determines the output meets a desired quality threshold. This can be seen as a form of _testtime compute_ , where additional inference cycles are used to improve reliability and performance. The trade-off is increased computational cost, but often with significantly better outcomes. This approach is especially effective in the following circumstances:

- There’s a clear evaluation rubric or checklist (e.g., correctness, completeness, tone).

- The cost of generating additional outputs is acceptable relative to the benefit of higher quality.

- The task is fuzzy or generative in nature, where a single attempt often underperforms a reranked or filtered approach.

In the supply chain example, an “actor” agent generates reorder plans and a “critic” evaluates for feasibility (e.g., cost, risk), which is repeated until approval. This subsequent code adds an actor-critic loop after the supervisor:

Actor-critic setups are particularly useful when evaluation is easier than generation. If you can reliably say “This is a good output,” but can’t easily produce it on the first try, then a simple actor-critic loop can be a powerful tool—no learning required. As an easy strategy to implement, it is often worth trying when a performance boost is worth the additional computational cost.

###### **Automated Design of Agent Systems**

Automated Design of Agentic Systems (ADAS) represents a transformative approach to agent development, shifting away from handcrafted architectures and toward systems that can design, evaluate, and iteratively improve themselves. As articulated by Shengran Hu, Cong Lu, and Jeff Clune in their 2024 original paper,<sup>1</sup> the central idea of ADAS is that, rather than manually constructing each component of an agent, we can enable a higher-level Meta Agent Search (MAS) algorithm to automatically create, assess, and refine agentic systems. This approach opens up a new research frontier—one that could enable agents to adapt to complex, shifting environments and continually improve their own capabilities without direct human intervention. As shows, ADAS builds on the idea that, historically, hand-designed solutions in machine learning (ML) have often been replaced by learned or automated alternatives, suggesting that agentic systems, too, may benefit from this transition.

In ADAS, foundation models serve as flexible, general-purpose modules within an agent’s architecture. These models, which already power strategies such as chain-ofthought reasoning, self-reflection, and Toolformer-based agents, form a base upon which more specialized or task-specific capabilities can be layered. However, ADAS seeks to advance beyond these traditional approaches by enabling agents to invent entirely new structures and modules autonomously. The versatility of foundation models provides an ideal starting point, but ADAS leverages automated processes to

> 1 Shengran Hu et al., “Automated Design of Agentic Systems”, paper presented at the International Conference on Learning Representations, Singapore, April 2025.

push beyond predefined capabilities, enabling agents to evolve novel prompts, control flows, and tool use. These building blocks are not static; rather, they are generated dynamically by the meta-agent, which can continuously experiment with new designs in response to changing requirements or opportunities for improvement.

The backbone of ADAS is the concept of defining agents through code. By utilizing programming languages that are Turing-complete, this framework theoretically allows agents to invent any conceivable structure or behavior. This includes complex workflows, creative tool integrations, and innovative decision-making processes that a human designer may not have foreseen. The power of ADAS lies in this code-based approach, which treats agents not as static entities but as flexible constructs that can be redefined, modified, and optimized over time. The potential of this approach is vast: in principle, a meta-agent could develop an endless variety of agents, continually refining and combining elements in pursuit of higher performance across diverse tasks.

Central to ADAS is the MAS algorithm, a specific method that demonstrates how a meta-agent can autonomously generate and refine agent systems. In MAS, the metaagent acts as a designer, writing code to define new agents and testing these agents against an array of tasks. Each successful design is archived, forming a continuously growing knowledge base that informs the creation of future agents. MAS operates through an iterative cycle: the meta-agent, conditioned on an archive of prior agents, generates a high-level design description, implements it in code (defining a “forward” function for the agent), and refines via two self-reflection steps for novelty and correctness. The new agent is evaluated on validation data; errors trigger up to five debugging refinements. Successful agents are archived with performance metrics (e.g., accuracy or F1 score), informing future iterations. This mirrors evolutionary processes, balancing exploration of novel designs with exploitation of high

performers. The meta-agent is thus both a creator and a curator, balancing exploration of new designs with exploitation of successful patterns. This process mirrors the evolution of biological systems, where successful traits are preserved and iteratively modified to adapt to new challenges.

To illustrate how MAS operationalizes these ideas, consider a generic Python implementation inspired by the open source ADAS. This framework uses a foundation model (e.g., GPT-5) as the meta-agent to generate and refine agent code. Key components include a foundation model agent base for prompting, a search loop for iterative evolution, and an evaluation function for fitness scoring. These elements enable the meta-agent to dynamically invent agents for tasks like grid puzzles (ARC [Abstraction and Reasoning Corpus]) or multiple-choice reasoning (MMLU), archiving high performers for future use:

The LLMAgentBase class forms the core of the meta-agent, wrapping interactions with a foundation model to generate structured responses (e.g., thoughts, code). It enforces JSON outputs for parseability and handles errors gracefully, allowing the metaagent to query for new agent designs based on archived priors. This modular design

ensures flexibility: the role (e.g., “helpful assistant”) and temperature (for creativity) can be tuned, while output descriptions guide task-specific behaviors, such as returning only a single-letter answer for MMLU.

At the heart of MAS is the search function, which iterates over generations to evolve agents. Starting from an initial archive (e.g., basic prompt-based agents), it conditions the meta-agent on past successes, generates new code, applies Reflexion for refinement, evaluates on validation data, and archives fitness-scored solutions. This loop balances exploration (novel designs) with exploitation (building on high performers), often running for 25–30 generations:

The evaluation function dynamically loads the generated agent’s code (via exec) as a callable forward function, applies it to task data in parallel (using multithreading for efficiency), and computes accuracy via task-specific scoring. This modular setup enables easy adaptation to new problems by subclassing a BaseTask abstract class, which defines methods for data loading, formatting, and prediction parsing. For example, in MMLU, it maps letter choices (A–D) to indices for exact-match scoring, while in ARC, it evaluates grid transformations for pixel-perfect accuracy. Such

implementations demonstrate the generality of ADAS, leading to the strong empirical results observed.

The results of MAS reveal an intriguing property of agents designed through ADAS: they tend to maintain high levels of performance even when applied to new domains and models. For instance, on the ARC challenge (grid-transformation puzzles), MASdiscovered agents outperformed hand-designed baselines like Chain-of-Thought (CoT), Self-Refine, and LLM-Debate. On reasoning benchmarks, MAS achieved F1 scores of 79.4 ± 0.8 on DROP (reading comprehension, +13.6 over Role Assignment baseline), 53.4% ± 3.5 accuracy on MGSM (math, +14.4% over LLM-Debate), 69.6% ± 3.2 on MMLU (multitask, +2% over OPRO prompt optimization), and 34.6% ± 3.2 on GPQA (science, +1.7% over OPRO). Cross-domain transfer was robust (e.g., ARC agents applied to MMLU), and performance held when switching models (e.g., from GPT-3.5 to GPT-4).

This robustness across domains suggests that agents created through MAS are not merely optimized for one-off tasks; rather, they embody more general principles and adaptive structures that enable them to excel even when the specifics of the environment change. This cross-domain transferability reflects a fundamental advantage of automated design: by generating agents that are inherently flexible, MAS produces solutions that can generalize more effectively than those designed for narrow, specialized contexts.

ADAS holds significant promise, yet its development requires careful consideration of both ethical and technical dimensions. The potential to automate the design of ever-more-powerful agents introduces questions about safety, reliability, and alignment with human values. While MAS offers a structured and exploratory approach, it is crucial to ensure that the evolving agents adhere to ethical standards and do not develop unforeseen behaviors that could be misaligned with human intentions. Ensuring that these systems are beneficial necessitates a balance between autonomy and constraint, giving agents the freedom to innovate while guiding them to operate within safe and predictable bounds.

The trajectory of ADAS suggests a future where agentic systems can autonomously adapt, improve, and tackle an expanding range of tasks with minimal human intervention. As ADAS advances, the ability of agents to develop more sophisticated designs will likely become a cornerstone of AI research, providing tools that can address increasingly complex, evolving challenges. In this way, ADAS offers a glimpse into a future of intelligent systems capable of self-improvement and innovation, embodying a shift from static, predesigned agents to adaptive, autonomous systems that grow alongside our expanding needs.

###### **Communication Techniques**

As agentic systems grow from single-agent prototypes into multiagent, distributed systems, the choice of communication architecture becomes increasingly critical. What starts as simple in-memory message passing or function calls quickly becomes untenable as systems grow in scope, number of agents, geographic distribution, or deployment complexity. This section explores the core techniques and technologies available for managing communication, coordination, and task flow across agents— especially as systems transition from single-device experiments to production-grade distributed deployments. The reader will notice there are many valid approaches, all with different trade-offs in development effort, latency, scalability, reliability, and cost.

###### **Local Versus Distributed Communication**

At a small scale—such as a single-device or single-process setup—agents often communicate through direct function calls, shared memory, or in-memory message queues. While simple and efficient, these methods don’t scale well. As soon as agents are distributed across services, containers, or nodes, communication must be made explicit, asynchronous, and fault-tolerant.

In local deployments, frameworks like AutoGen often use in-memory routers to orchestrate agent message passing and tool invocation. These setups can work well for research and prototyping, especially with single-threaded or single-agent configurations. But for production use, communication and state management must evolve.

###### **Agent-to-Agent Protocol**

The Agent-to-Agent (A2A) Protocol, introduced by Google, is an ambitious and promising step toward enabling autonomous agents to work together toward more complex goals. It offers a standardized, cross-platform mechanism for agents to discover each other, negotiate collaboration, and exchange structured requests—without revealing internal logic or implementation details. By enabling heterogeneous agents to interoperate over HTTP-based transports, A2A creates a shared language that could, in time, make multiagent coordination as routine as API calls between microservices.

At the core of A2A is the _Agent Card_ , a machine-readable JSON descriptor that each agent publishes to advertise its identity, capabilities, endpoints, and supported authentication methods. These cards enable agents to find peers, evaluate their functions, and negotiate secure communication channels. Capabilities are defined explicitly—such as generateReport , summarizeLegalDocument —along with schemas for inputs and outputs, enabling structured composition of agent workflows. Endpoint information and supported authentication methods (e.g., OAuth 2, API key) ensure

that communication can be established securely and programmatically. Optional metadata like versioning and media support further enrich agent discovery and compatibility. To illustrate, here’s a simple Python dictionary representing an Agent Card for a summarization agent:

This JSON can be served at a well-known endpoint like _/.well-known/agent.json_ for discovery. A2A uses JSON-RPC 2.0 over HTTPS as its reference implementation, but the protocol is designed to be transport-agnostic. This opens the door to integration over gRPC, WebSocket, or other streaming and multiplexed protocols as infrastructure demands evolve. JSON-RPC ensures consistent handling of requests, responses, and errors, creating a shared semantic model even across agents built in different languages or frameworks.

In practical use, agents locate one another via a registry—centralized or distributed— that stores Agent Cards. Once a peer is identified, an initiating agent performs a handshake, exchanging Agent Cards and negotiating session parameters like protocol version, timeout expectations, or payload limits. For example, a client agent might discover and negotiate compatibility like this (using Python’s requests library):

Once validated, the agents can begin coordinating work: Agent A may issue a request Summarize call to Agent B, who then processes the request and returns a structured response or an error, as needed. Continuing the example, here’s how the client issues a JSON-RPC request:

On the server side, handling this request might look like this (using Python’s http.server for simplicity):

While A2A presents an exciting direction for multiagent systems—offering a modular, runtime-agnostic approach to delegation and coordination—it is still in its infancy. Significant open questions remain, particularly around security. Authentication is currently supported via pluggable mechanisms, but robust authorization, ratelimiting, trust establishment, and abuse resistance are far from solved. As with any early protocol, it should be approached with both enthusiasm and caution. Early adopters should expect vulnerabilities, implementation gaps, and evolving specifications.

Still, A2A points to a future where agents don’t operate in isolation but as part of dynamic, loosely coupled ecosystems capable of tackling broader and more sophisticated problems. Much like HTTP enabled the composability of the web, A2A aspires to do the same for AI agents. It’s too early to say whether it will become _the_ standard—but it’s a promising beginning in the quest to make agent cooperation seamless, scalable, and secure.

###### **Message Brokers and Event Buses**

As agent-based systems scale, point-to-point communication becomes brittle and inflexible. A common alternative is to adopt message brokers or event buses, which

decouple senders from receivers and enable agents to interact asynchronously through a shared communication fabric. This pattern establishes scalable, faulttolerant, and observable workflows, especially in loosely coupled multiagent architectures.

To see the utility of this approach, consider integrating a message broker into a supply chain multiagent system from earlier in this chapter. In the original synchronous setup, the supervisor directly routes to a specialist via graph edges, creating tight coupling. By using a broker, the supervisor can publish tasks to a shared topic (e.g., “supply-chain-tasks”), and specialists subscribe asynchronously—processing only relevant messages. This decouples agents, enabling independent scaling (e.g., replaying inventory instances), fault tolerance (e.g., replay missed messages), and easier addition of new agents without rewriting the graph. Key options include:

###### _Apache Kafka_

This is a high-throughput, distributed event streaming platform ideal for agent systems where agents need to publish and consume structured events. Kafka supports strong durability, topic partitioning for parallelism, and consumer groups for coordination. It is especially effective for building log-based communication architectures where every interaction is preserved and replayable.

###### _Redis Stream and RabbitMQ_

These are lightweight alternatives for lower-throughput or simpler use cases, with tighter latency and easier deployment. Redis Stream in particular offers fast, memory-based communication, though durability is more limited.

###### _Neural Autonomic Transport System (NATS)_

A lightweight, cloud-native messaging system designed for low-latency, highthroughput communication. NATS is ideal for real-time agent coordination in microservice or edge environments. It supports publish/subscribe, request/reply, and—with JetStream—durable message streams and replay. NATS emphasizes simplicity, speed, and scalability, making it well suited for distributed agentic systems that require fast, resilient communication with minimal overhead.

For the supply chain agent system, Redis Stream provides quick, low-latency decoupling ideal for prototyping. The supervisor adds tasks to a stream, and specialists read/consume them in separate processes. Assume Redis is running (e.g., via Docker: docker run -p 6379:6379 redis ) and use redis-py ( pip install redis ). The supervisor determines the specialist and publishes the task:

Specialists (e.g., inventory) consume in a loop, process with their node logic, and publish responses:

We then set up similar consumer loops to run for transportation and supplier specialists. To wait for a response:

In general, it’s wise to run specialists in separate processes (e.g., via multiprocessing). This enables fast async coordination—e.g., the supplier agent can process compliance tasks without blocking others—while keeping setup simple for lower-scale systems.

Message buses support loose coupling between agents, allowing for flexible scaling, observability via logging pipelines, and replay of failed or missed messages. However, they also introduce challenges around eventual consistency and the need for more complex error handling.

###### **Actor Frameworks: Ray, Orleans, and Akka**

While message buses primarily decouple communication by routing events asynchronously between components—focusing on data flow without dictating execution— actor frameworks integrate both messaging and computation into a unified model. Here, actors (representing agents) not only exchange messages but also encapsulate their own state and behavior, ensuring sequential processing to eliminate race conditions and shared-state bugs common in traditional threaded systems. This contrasts sharply with the standard monolithic approach many developers initially take: deploying a single-container agent service that handles all logic centrally, often relying on synchronous foundation model calls and in-memory orchestration. While simple for prototypes, such setups become bottlenecks at scale—prone to single points of failure, inefficient resource use during idle periods, and challenges in parallelizing diverse agent roles without custom concurrency hacks.

Actor frameworks shine in scenarios requiring fine-grained distribution, resilience, and dynamic scaling, such as multiagent simulations with persistent per-agent memory (e.g., tracking conversation history or learned behaviors), high-concurrency

environments like real-time bidding or IoT coordination, or systems integrating heterogeneous agents across clusters. They enable “location-transparent” invocation— where actors can migrate or replicate without changing code—and built-in supervision for automatic recovery from failures, reducing operational overhead compared with manually managing queues or containers.

The investment in infrastructure (e.g., setting up clusters, monitoring actor lifecycles) pays off when systems exceed a few agents or handle variable workloads: for instance, in production agent swarms where downtime costs are high, or when evolving from local prototypes to cloud native deployments. For smaller, low-traffic setups, the added complexity may not justify it—stick to buses or monolithic services—but as the agent count grows beyond 10–20 or latency demands tighten, actors provide unmatched elasticity and fault tolerance. Three leading frameworks in this space are Ray, Orleans, and Akka, each offering distinct advantages depending on the environment and language ecosystem:

###### _Ray_

Ray is a Python-native distributed computing framework that supports an actor model for stateful, scalable computations. Actors in Ray are defined using the @ray.remote decorator, enabling asynchronous method invocations that process messages while preserving internal state across invocations. Ray manages distribution automatically, with resource-aware scheduling, fault tolerance via optional restarts and retries, and support for clustering to handle large-scale deployments. It pairs naturally with tools like AutoGen or LangGraph for agentic systems, offering a lightweight alternative in Python environments where ease of use and rapid prototyping are prioritized over JVM-specific (Java Virtual Machine) performance tuning.

###### _Orleans_

Orleans offers a _virtual actor model_ , where actors (or agents) are logically addressable and automatically instantiated, suspended, or recovered based on demand. Orleans handles state persistence, concurrency, and lifecycle management with minimal boilerplate. It abstracts away much of the complexity of distributed systems while enabling developers to scale agent-like components naturally across a cluster. When paired with AutoGen, Orleans can power agent systems that treat each agent as a service, dynamically scaling with system needs while retaining internal state and identity.

###### _Akka_

Akka is a well-established actor framework in the JVM ecosystem, supporting both Java and Scala. Akka’s classic actor model is highly performant and suitable for building fault-tolerant, distributed systems with fine-grained control over actor behavior. With Akka Cluster, actors can be distributed across multiple nodes, supporting advanced features like sharding, persistence, supervision, and

adaptive load balancing. Akka is particularly well suited for high-throughput, low-latency applications requiring tight control over concurrency, and it has been used in production environments ranging from telecom systems to trading platforms.

This actor-style design aligns naturally with multiagent coordination, where each agent maintains its own identity, role, and internal state. Actor systems enable these agents to be invoked dynamically, react to messages or events, and manage complex workflows through message passing rather than shared state or global control.

Because this book emphasizes Python-based implementations for multiagent systems (e.g., using LangChain and related libraries), we’ll illustrate the actor model with a Ray example integrated into the supply chain system. Similar principles apply to Orleans (primarily .NET-based, ideal for Windows ecosystems or enterprise integrations) and Akka (JVM-focused, suited for high-performance Java/Scala apps), but their code would require language-specific adaptations beyond our Python-centric scope.

In the context of the supply chain multiagent system, the specialist agents (e.g., inventory, transportation) are implemented as Ray actors with per-session isolation. Each session (identified by operation_id ) gets its own actor instance per specialist type, ensuring clean state management—isolated history or caches per session—while guaranteeing sequential execution within each actor for tasks in that session. This avoids cross-session contamination and enables parallel processing across sessions in a cluster. A session manager actor tracks and creates these on demand. Here’s the core Ray actor class for a specialist, which processes tasks sequentially and maintains isolated session state:

This actor encapsulates the foundation model and tool logic, processing messages (tasks) serially via process_task —Ray queues concurrent calls to the same actor and executes them one by one, preserving order and state integrity. The internal_state dict is session-isolated because each actor is created per session, enabling per-session persistence (e.g., step tracking) without shared memory risks. A session manager actor handles dynamic creation for isolation:

For developers building agentic systems, actor frameworks like Orleans and Akka offer a proven, scalable foundation for representing each agent as an autonomous, self-contained unit—capable of handling asynchronous workflows, maintaining persistent memory, and integrating cleanly into distributed infrastructures.

###### **Orchestration and Workflow Engines**

Even with robust messaging and agent execution models, real-world systems need orchestration—the logic that sequences tasks, handles retries, tracks dependencies, and manages failure across agents. This is especially important for long-running or multistep interactions that span time and components. Workflow orchestration tools provide a higher-level abstraction, ensuring durability and recoverability in complex agentic systems.

Workflow orchestration tools are particularly useful when processes involve unreliable external dependencies (e.g., APIs, foundation models, or human approvals), potential failures, or extended durations—such as supply chain workflows that may take days due to asynchronous agent actions or real-world delays. By persisting state and automating recovery, these engines prevent data loss and redundant work, making them essential for production-grade reliability where simple in-memory coordination falls short. Use them when scaling from prototypes to resilient deployments, especially in scenarios with high stakes like financial transactions, compliance-heavy operations, or distributed AI agents; for quick, low-risk experiments, basic scripting may suffice.

Temporal provides durable, stateful workflows with long-running tasks, retries, and failure recovery. It’s ideal for managing multiagent systems where each agent may perform asynchronous, multistep actions. Temporal workflows offer a clean abstraction for encapsulating business logic that spans multiple services or agents over long durations.

To illustrate Temporal’s durable execution in the supply chain multiagent system, consider a workflow that sequences agent steps (e.g., inventory management, then transportation arrangement, followed by supplier compliance)—with automatic retries on failures and persistent state for recovery. Temporal ensures the workflow resumes from the last successful step even after crashes, making it suitable for

production agent coordination. Assume Temporal is set up (e.g., via pip install temporalio ), with activities defined for each specialist (wrapping their foundation model/tool logic). Here’s a simplified workflow definition:

This workflow durably sequences the agents. Each activity (agent step) runs with retries, and Temporal persists progress—e.g., if transportation fails, it retries without

rerunning inventory. For long-running processes, add signals for user input or pauses, similar to the full example’s confirmation handling.

Apache Airflow is widely used for data pipelines but can also coordinate agent flows via DAGs (directed acyclic graphs). While powerful, Airflow is best suited to batch or time-triggered workflows. Airflow remains a staple for scheduled, tool-agnostic orchestration in data engineering and business operations, such as ETL (extract, transform, load) jobs or ML model training. Opt for Airflow when dealing with periodic, dependency-heavy pipelines that benefit from its mature ecosystem and visualization tools, but not for real-time or highly dynamic agent interactions.

For developers preferring to prototype and run orchestration locally before scaling to distributed environments, tools like Dagger can be particularly useful, enabling workflows to be composed as code using containers, foundation models, and other resources with automatic caching and type safety. This ensures consistency across local development, CI/CD pipelines, and production, and even supports agentic integrations such as automation enabled by foundation models, making it a flexible option depending on your stack. Workflow engines offer a higher layer of abstraction —separating coordination logic from communication mechanics. They help ensure idempotency, recoverability, and durable state—features that become essential when agents fail, stall, or must respond to changing environments.

###### **Managing State and Persistence**

Communication alone is not enough—multiagent systems must also manage shared state, agent memory, and task metadata that often span multiple executions, workflows, or system restarts. This introduces significant complexity in terms of data durability, consistency, and access patterns, particularly as the system scales.

As you can see in Table 8-1, traditional solutions rely on stateful databases like PostgreSQL, Redis, or vector stores to persist task outcomes, interaction logs, and agent memories. These offer fine-grained control and can be tailored to the needs of each agent, but they also require developers to explicitly manage schema design, read/ write consistency, caching, and recovery logic—adding engineering overhead and opportunities for subtle bugs.

For unstructured or large-scale outputs (e.g., plans, tool traces, JSON blobs), object storage options like Amazon S3 or Azure Blob Storage provide durable, low-cost storage with high availability. This is ideal for immutable artifacts, but it comes with trade-offs in access latency and the need for separate indexing or tracking systems to relate artifacts back to agent tasks or states.

_Table 8-1. Durable storage option overview_

Frameworks like Temporal and Orleans offer a different approach: they abstract away much of the complexity of persistence by tightly integrating state management into the agent or workflow lifecycle. Temporal automatically checkpoints workflow progress, supports deterministic replay, and handles failures transparently. Orleans enables each actor (agent) to maintain a durable, event-driven state with minimal boilerplate. These abstractions reduce development effort and improve resilience, but they also impose framework-specific constraints—such as serialization formats, execution models, or language bindings—that may not suit every architecture.

The right choice depends on the nature of the memory and coordination required:

- Episodic memory (short-lived, task-specific state) may only need in-memory or transient storage with minimal durability.

- Semantic memory (long-term knowledge across interactions) typically requires durable storage with search or vector indexing capabilities.

- Workflow durability (resilience to mid-process failure) benefits most from integrated engines like Temporal or Orleans that automatically checkpoint progress and state.

Ultimately, persistence decisions reflect trade-offs between developer effort, performance, durability, and flexibility. Systems with tight service-level agreements, crossagent dependencies, or real-time coordination requirements will often benefit from workflow-native persistence layers, while more modular or research-oriented systems may prefer explicit, database-driven state management that offers more control and visibility.

###### **Conclusion**

The transition from single-agent to multiagent systems offers significant advantages in addressing complex tasks, enhancing adaptability, and increasing efficiency. Yet, as we’ve explored in this chapter, the scalability that comes with adding more agents brings challenges that demand careful planning. Deciding on the optimal number of

agents requires a nuanced understanding of task complexity, potential task decomposition, and the cost-benefit balance of multiagent collaboration.

Coordination is critical to success in multiagent systems, and a variety of coordination strategies—such as democratic, manager-based, hierarchical, actor-critic approaches, and automated design with ADAS—provide different trade-offs between robustness, efficiency, and complexity. Each coordination strategy offers unique advantages and limitations, suited to particular scenarios, and careful selection can significantly enhance a system’s effectiveness and reliability.

Equally critical is the choice of communication infrastructure. As systems scale, so too does the need for reliable, low-latency, and durable message passing between agents. While in-memory queues may suffice in simple settings, production-grade systems often rely on message brokers (e.g., Kafka, NATS, RabbitMQ), actor frameworks (e.g., Orleans, Akka), and workflow engines (e.g., Temporal, Conductor) to manage not only communication but also state, retries, and execution durability. Designing for effective communication is not just an implementation detail—it is a first-class concern that shapes how agents perceive, respond to, and collaborate within their environment. To help developers navigate these options, Table 8-2 summarizes the key communication and execution approaches for multiagent systems, comparing their concepts, trade-offs, and ideal use cases in the context of our supply chain example.

_Table 8-2. Agent coordination techniques_

By understanding these factors and applying them thoughtfully, developers can create multiagent systems that are not only robust and capable but also prepared to meet the demands of increasingly complex, dynamic tasks in real-world applications. This strategic approach enables multiagent systems to evolve as powerful solutions that drive meaningful advancements across various domains.

### **CHAPTER 9 Validation and Measurement**

It has never been easier to build products and applications, but effectively measuring these systems remains an enormous challenge. While teams are often under pressure to ship things quickly, taking the time to rigorously evaluate performance and assess quality pays long-term dividends and enables teams to ultimately move faster and with more confidence. Without rigorous evaluation and measurement, decisions about which changes to ship become much more difficult. Rigorous measurement and validation become essential, not only to optimize performance but also to build trust and ensure alignment with user expectations.

This chapter explores methodologies for evaluating agent-based systems, covering key principles, measurement techniques, and validation strategies. We explore the critical role of defining clear objectives, selecting appropriate metrics, and implementing robust testing frameworks to assess system performance under real-world conditions. Beyond mere functionality, the reliability of agent outputs—including accuracy, consistency, coherence, and responsiveness—requires systematic scrutiny, particularly given the probabilistic nature of foundation models that often power these systems.

Throughout this chapter, we follow a customer support agent handling a common ecommerce scenario: a customer reports a cracked coffee mug and requests a refund. We’ll build on this case, exploring variations like multi-item orders, cancellations, or changes in addresses, to illustrate measurement, validation, and deployment.

###### **Measuring Agentic Systems**

Without rigorous measurement, it is impossible to ensure that the system meets its intended goals or handles the complexities of real-world environments. By defining clear objectives, establishing relevant metrics, and employing systematic evaluation

processes, developers can guide the design and implementation of agent systems toward achieving high performance and user satisfaction.

###### **Measurement Is the Keystone**

Effective measurement begins with identifying clear, actionable metrics that align with the goals and requirements of the agent system. These metrics serve as the benchmarks for evaluating the agent’s ability to perform tasks and meet user expectations. Success depends on defining specific, measurable objectives that reflect the desired outcomes for the system, such as enhancing user engagement or automating a complex process. By framing hero scenarios—representative examples of highpriority use cases—developers can ensure their metrics target the core functions that define the agent’s success. In the absence of rigorous and ongoing measurement, it becomes impossible to know whether changes are truly improvements, to understand how agents perform in realistic and adversarial settings, or to guard against unexpected regressions.

Selecting the right metrics is equally crucial. Metrics should encompass a combination of quantitative indicators, such as accuracy, response time, robustness, scalability, precision, and recall, as well as qualitative measures like user satisfaction. For example, in a customer service agent, response time and accuracy might measure performance, while user feedback captures overall satisfaction. These metrics must reflect the real-world demands the system will face.

In the case of language-based agents, traditional exact-match metrics frequently fail to capture genuine utility, as correct answers can take many forms. As a result, modern practice relies increasingly on semantic similarity measures—such as embedding-based distance, BERTScore, BLEU (Bilingual Evaluation Understudy), or ROUGE (Recall-Oriented Understudy for Gisting Evaluation)—to evaluate whether agent outputs truly meet the intent of a given task, even if the wording diverges from a reference answer.

To realize the benefits of measurement, it is crucial to integrate evaluation mechanisms directly into the agent-development lifecycle. Rather than relegating evaluation to the end, successful teams automate as much as possible, triggering tests whenever new code is merged or models are updated. By maintaining a consistent source of truth for key metrics over time, it becomes possible to detect regressions early, preventing new bugs or degradations from reaching production. Automated evaluation, however, rarely tells the whole story. Particularly in novel or high-stakes domains, regular sampling and human-in-the-loop review of agent outputs can uncover subtle issues and provide a qualitative sense of progress or remaining challenges. The most effective teams treat evaluation as an iterative process, refining both their agents and their metrics in response to ongoing feedback and changing requirements.

###### **Integrating Evaluation into the Development Lifecycle**

Measurement must not be an afterthought, nor can it be left to informal methods such as simply “eyeballing” outputs or relying on gut instinct. In the absence of systematic evaluation, it is all too easy for even expert teams to fool themselves into believing their agentic systems are improving, when in fact progress is illusory or uneven. Leading teams integrate automated, offline evaluation into every stage of development. As new tools or workflows are added to an agent, corresponding test cases and evaluation examples should be added to a growing evaluation set. This disciplined approach ensures that progress is measured not just against a fixed benchmark, but across the expanding scope of the system’s capabilities.

High-quality evaluation sets can act as a living specification for what the agent must handle, supporting reproducibility and regression detection as the system evolves. By tracking historical results on these evaluation sets, teams can identify when apparent improvements come at the cost of newly introduced errors or degradations elsewhere in the system. In contrast to ad hoc or manual review, this rigorous practice enforces a culture of accountability and provides a quantitative foundation for decision making. Ultimately, it is the careful curation and continual extension of evaluation sets— matched to both legacy and emerging features—that enables teams to maintain trust in their metrics and ensures that agentic systems are truly advancing toward their intended goals.

###### **Creating and Scaling Evaluation Sets**

The foundation of any measurement strategy is a high-quality evaluation set—one that reflects the diversity, ambiguity, and edge cases the system will face in the real world. Static, hand-curated test suites are insufficient for modern agentic systems: they risk overfitting, miss long-tail failure modes, and can’t keep pace with evolving workflows and user behaviors.

A good evaluation set defines both the input state and the expected outcome, enabling automated validation of agent behavior. Consider this illustrative example from a customer support agent, which extends our cracked mug scenario, now with multiple items:

This single example tests several things at once. It verifies whether the agent can reason correctly over multi-item orders, match conversational context to tool use, and produce human-friendly confirmations. Evaluation metrics such as tool recall, parameter accuracy, and phrase recall quantify these behaviors. If the agent instead refunded the entire order or failed to include appropriate language in its final message, those metrics would reflect the error—providing precise, actionable signals for improvement.

By formalizing evaluation examples in a structured format—including input state, conversation history, and expected final state—teams can automate scoring and aggregate metrics across a wide variety of scenarios. This format scales well. Once established, new examples can be added by hand, mined from production logs, or even generated using foundation models. Language models can be prompted to introduce ambiguity, inject rare idioms, or mutate working examples into edge cases. These model-generated samples can then be reviewed and refined by humans before inclusion in the test set.

To push the boundaries further, teams can apply targeted generation techniques such as adversarial prompting (e.g., “Find a user message that causes the agent to contradict itself”), counterfactual editing (e.g., “Change one word in the prompt and see if the agent fails”), or distributional interpolation (e.g., “Blend two intents to create a deliberately ambiguous request”). These strategies uncover subtle errors and probe the robustness of agent behavior.

In domains with access to real-world data, such as customer support logs or API call traces, domain-specific mining provides another rich source of evaluation material.

Meanwhile, standard benchmarks like MMLU, BBH, and HELM can help contextualize performance relative to broader trends in the field, even as custom benchmarks remain essential for domain-specific agents.

Over time, a well-structured evaluation set becomes more than a test suite—it becomes a living specification of what the agent is expected to handle. It supports regression detection, enables continuous monitoring, and drives real progress by ensuring that agent behavior is improving not only on average, but in the places that matter most. This approach transforms evaluation from a static gatekeeping function into a dynamic, model-driven feedback loop that directly shapes the trajectory of system development.

For novel domains, teams should invest in custom benchmark creation, often pairing engineers with subject matter experts to define tasks, ground truth, and success criteria. This includes metadata for downstream analysis, such as failure type tagging or coverage tracking.

Regular evaluation against this continuously evolving evaluation corpus provides a scalable way to detect regressions, surface systemic weaknesses, and quantify improvements with statistical rigor.

This approach transforms evaluation from a static question-answer gate into a dynamic, model-driven feedback loop.

###### **Component Evaluation**

Unit testing is a fundamental practice in software development and is critical for validating the individual components of agent-based systems. Effective unit tests ensure that each part of the system functions as intended, contributing to the overall reliability and performance of the agent.

###### **Evaluating Tools**

Tools are the core functions that empower agents to act on their environment, retrieve or transform data, and interact with external systems. High-quality unit testing for tools begins with exhaustive enumeration of use cases, encompassing not only the typical “happy path” but also rare, adversarial, or malformed scenarios that could reveal brittle edges or hidden assumptions.

A mature agent development process defines a suite of automated tests for every tool. For instance, a data retrieval tool should be tested across different data formats, varied network conditions, and with both valid and intentionally corrupted data sources. Testing should explicitly validate not just the correctness of outputs but also latency, resource consumption, and error handling—ensuring that the tool degrades gracefully under load or failure.

Tool tests should assert that outputs are deterministic for identical inputs unless stochasticity is part of the tool’s design (in which case, statistical properties must be checked). For tools with external dependencies, such as APIs or databases, developers should use mocks or simulators to reproduce edge cases that might be rare in production but catastrophic if mishandled. Regression tests are critical; every time a tool is modified, the full suite of tests must be rerun to verify that past capabilities have not broken.

###### **Evaluating Planning**

Planning modules transform high-level goals into actionable sequences of steps— often involving dynamic decision making, branching logic, and adaptation to environmental feedback. Unlike traditional scripts, agentic planning is often probabilistic or adaptive, requiring careful testing to avoid brittle or inconsistent behaviors. A planner might need to sequence tool calls, coordinate conditionals, or stop early depending on what it learns during execution. This makes validation both more subtle and more essential.

To assess planning quality, we begin with canonical workflows: common, wellunderstood user intents paired with known-good agent responses. For each scenario, we encode the starting environment, a conversation history, and the expected outcome in terms of tool usage and user communication. In the case of our customer support agent, for example, when a customer requests a refund for a damaged mug, the planner should determine that issuing a refund is the right action, not canceling the order or modifying an address. It should also include a confirmation message in natural language that reassures the customer that the issue has been resolved.

To evaluate these plans systematically, we run the agent end-to-end and extract its chosen actions. Specifically, we capture the list of tool invocations and their arguments from the agent’s generated outputs. These are compared against the ground truth expectations for the scenario. From this comparison, we compute several automated metrics:

###### _Tool recall_

Did the planner include all expected tool invocations?

###### _Tool precision_

Did it avoid calling tools that were unnecessary?

###### _Parameter accuracy_

For each tool, did it supply the correct arguments—such as the specific order ID or refund amount?

These metrics provide fine-grained insight into the planner’s behavior. A low recall score might indicate the planner failed to take an essential action, while low precision suggests it misunderstood the goal or misread the user’s intent. Parameter

mismatches can highlight failures of contextual grounding—such as refunding the wrong item or issuing a refund for an order that was delivered successfully:

Because planning often depends on context, it is especially important to test edge cases. What if the order contains multiple items, and only one is defective? What if the user provides ambiguous input or contradicts themselves across messages? Tests should cover these situations to ensure the planner can navigate ambiguity and recover from intermediate failures.

Planning modules should also be evaluated for consistency. In deterministic scenarios, the same input should produce the same output; in probabilistic cases, the range of plans should still fall within acceptable bounds. Tests can check for reproducibility, sensitivity to small input changes, and graceful handling of unexpected conditions— such as missing fields in an order object or failed tool execution.

Over time, we maintain a growing corpus of planning scenarios that reflect the full range of what the agent must support—from simple, single-step flows to complex multiturn dialogues involving multiple interdependent actions. This corpus becomes the backbone of integration testing for planning. By continuously evaluating planning behavior as the system evolves, we detect regressions early and ensure that new capabilities do not introduce instability or drift.

Ultimately, planning evaluation tells us whether the agent knows what to do. It confirms that the agent not only understands user intent but can convert that intent into precise, coherent, and contextually grounded actions. As the bridge between

perception and execution, planning must be scrutinized carefully—because everything downstream depends on it.

###### **Evaluating Memory**

Memory is essential for agents that need continuity and contextual awareness, whether for multiturn conversations, long-running workflows, or persistent user profiles. Testing memory modules is nontrivial, as it involves not only verifying raw storage and retrieval but also ensuring data integrity, relevance, and efficiency as the memory store grows.

Unit tests for memory should first verify that data written to memory is accurately stored and can be precisely retrieved, both immediately and after significant time has elapsed or other operations have intervened. This includes boundary cases such as maximum memory capacity, unusual data types, or rapid-fire read/write cycles. Tests should intentionally stress the system with malformed, duplicate, or ambiguous entries to ensure robustness:

Beyond correctness, memory modules must be tested for relevance—ensuring that retrieval logic does not surface stale or irrelevant information. For instance, if the agent is asked for a user’s recent preferences, the test must confirm that outdated or incorrect preferences are not returned due to data leakage or indexing errors. Tests should also check that irrelevant but similar data is not retrieved simply because of superficial similarity in phrasing or semantics.

Efficiency is a critical dimension, especially as memory size grows. Developers should benchmark retrieval times and resource usage under increasing memory loads,

identifying any performance cliffs or bottlenecks. If vector search or semantic memory is used, tests should include scenarios with both “easy” and “hard” retrievals to catch subtle errors in embedding or indexing logic.

Finally, memory systems must be resilient to partial failures. Tests should simulate database unavailability, data corruption, or version migrations to ensure that the agent either recovers gracefully or fails in a controlled manner, with minimal user impact.

###### **Evaluating Learning**

Learning components are perhaps the most complex to unit test, given their stochastic nature and dependence on data. Nevertheless, rigorous testing is crucial to ensure that agents genuinely improve over time and do not simply overfit, regress, or “forget” previously mastered behaviors.

Testing learning begins with verification of the basic learning loop: does the agent correctly update its parameters, cache, or rules in response to labeled data, feedback, or reward signals? For agents employing supervised learning, unit tests should confirm that, when trained on a canonical dataset, the agent achieves expected accuracy and generalizes correctly to validation data. For reinforcement learning agents, tests should check that reward maximization leads to improved behavior over time, and that learning plateaus are detected and handled (e.g., through early stopping or dynamic exploration).

Generalization is paramount. Tests should evaluate how well the agent applies learned behaviors to novel, out-of-distribution scenarios. This includes “holdout” sets, synthetic examples, or adversarial test cases specifically constructed to challenge brittle heuristics or memorized responses.

Adaptability is also vital. Tests should simulate distribution shifts—such as new types of user inputs, previously unseen tool failures, or changing reward landscapes—and confirm that the agent can adapt without catastrophic forgetting or performance collapse. Where appropriate, learning modules should be tested across multiple paradigms (supervised, unsupervised, reinforcement), ensuring that cross-paradigm interactions do not introduce subtle bugs.

By rigorously testing these components—tools, planning, memory, and learning— developers can ensure that the foundational elements of the agent-based system operate reliably and effectively. This comprehensive approach to unit testing provides the confidence needed to build robust and scalable agents for real-world applications.

###### **Holistic Evaluation**

While unit tests validate the correctness of individual components in isolation, integration tests are designed to evaluate the agentic system as a whole, ensuring that all subsystems—tools, planning, memory, and learning—work together seamlessly in realistic settings. Integration testing exposes complex interactions, emergent behaviors, and end-to-end issues that cannot be predicted from unit testing alone. In agentbased systems, where the outputs of one module often become the inputs for another, integration tests are essential for surfacing problems that arise only during real-world use.

###### **Performance in End-to-End Scenarios**

The primary objective of integration testing is to validate the system’s ability to perform complete tasks from start to finish, under conditions that closely resemble actual usage. This involves constructing representative workflows or user journeys that exercise the full stack of the agentic system—perception, planning, tool invocation, and communication. For example, a customer support agent might be tested on multistep conversations that involve interpreting user requests, making decisions based on order data, calling business tools like issue_refund , and providing appropriate follow-up messages to the customer. These evaluations must ensure that the agent not only selects the right actions but also communicates clearly and stays aligned with user intent.

In our framework, this kind of evaluation is operationalized through an evaluate_single_instance function, which executes a complete test case and computes a set of metrics. The agent is given a structured input—including the order data and conversation history—and its outputs are compared against an expected final state. This includes checking which tools were called, with what parameters, and whether the final message includes required phrases. The results are summarized in metrics such as tool recall, tool precision, parameter accuracy, phrase recall, and an aggregate task success score. This makes it possible to assess the agent’s full behavior —did it understand the situation, take the right actions, and explain them well? The following code is a helper function that executes an end-to-end integration test for a single scenario—invoking the agent on structured input and computing metrics for tool usage, parameter accuracy, phrase recall, and overall task success:

This approach enables scalable, repeatable measurement of end-to-end agent behavior across dozens or hundreds of diverse scenarios. A critical limitation is that automated tests are only as good as the evaluation sets and metrics they employ. If test cases are too narrow or unrepresentative, agents may appear to perform well in offline testing yet fail in production. Similarly, overreliance on a small set of metrics can lead to “metric overfitting,” where systems are tuned to excel on benchmarks at the expense of broader utility. This is particularly common with text-based agents, where optimizing for a single score (such as BLEU or exact match) may incentivize formulaic or unnatural outputs that miss the true intent behind user requests.

The best practice is to treat evaluation as a living process, not a static checklist. Teams should regularly expand and refine test sets to reflect new features, real user behavior,

and emerging failure modes. Incorporating feedback—from internal reviewers or pilot users—helps reveal blind spots that automated pipelines miss. Iterative refinement of both evaluation methods and metrics ensures that agents are measured against what truly matters for success in the target environment.

By structuring each evaluation as a complete interaction—from input state to agent outputs—we can track how well the system performs in real-world tasks, detect regressions over time, and surface weaknesses in planning, grounding, or communication. These tests can also be extended to capture latency, throughput, and behavior under load—ensuring that the system remains robust and responsive under realistic operating conditions. And in failure cases, we can validate whether the agent degrades gracefully: does it attempt fallback strategies or escalate the issue appropriately? In this way, integration testing becomes a rigorous and essential safeguard for deploying agentic systems with confidence.

###### **Consistency**

Consistency testing for agent-based systems is particularly challenging because these systems often rely on foundation models that are inherently probabilistic and nondeterministic. Unlike traditional systems, where deterministic behavior ensures the same outputs for identical inputs, LLM-powered agents may produce varied responses due to their probabilistic nature. As a result, consistency testing focuses on ensuring that the agent’s outputs align with its inputs, remain coherent over extended exchanges, and reliably address the user’s intended questions or tasks.

One key goal of consistency testing is to validate that the agent’s responses remain aligned with the given input across diverse scenarios. This involves assessing whether the agent provides relevant and accurate answers that directly address the user’s queries. Automated tools can help detect cases where responses deviate from the expected alignment. Automated validation systems can cross-check outputs against the input context to flag inconsistencies for further review.

Longer interactions introduce additional complexity, as performance may degrade over time. Agents must maintain logical progression across multiturn conversations, avoiding scenarios where their responses contradict earlier statements or stray from the topic at hand. For example, a customer service bot must preserve context throughout an interaction, ensuring that its responses are consistent with the user’s

earlier inputs and the overall goal of the exchange. Testing in this area often requires extended simulated conversations to evaluate the system’s ability to sustain consistent performance over time.

A subtle risk is that automated evaluations can miss rare but critical edge cases, especially those arising from novel inputs or system interactions. Agents may “pass” all standard tests but still behave unpredictably when confronted with situations outside the test set’s distribution. For this reason, ongoing manual inspection and periodic refreshment of evaluation data are vital.

Both automated and human reviews play essential roles in addressing these challenges. Human reviewers can assess nuanced inconsistencies and provide feedback on how well the agent adheres to the intended purpose of its responses. This process is particularly important for evaluating edge cases or ambiguous inputs where automated systems may fall short. At the same time, scalable validation can be achieved through LLM-based evaluation techniques. By using the same or related models for consistency checking, agents can assess their own outputs against expectations. Providing these evaluation models with few-shot examples of what constitutes a consistent and relevant response enhances their reliability.

Actor-critic approaches offer another valuable tool for consistency testing. In this framework, the “actor” generates responses, while the “critic” evaluates them against predefined criteria for alignment and relevance. While effective, these methods alone may not suffice for complex or highly dynamic scenarios. The combination of actorcritic evaluations with LLM-based assessments and human feedback creates a more comprehensive framework for identifying and addressing inconsistencies.

Consistency testing ultimately ensures that agent-based systems deliver outputs that are aligned, logical, and purposeful, even in the face of nondeterministic behavior. By leveraging a mix of automated validation, human oversight, and advanced evaluation techniques like actor-critic frameworks and LLM-driven assessments, developers can build systems that inspire trust and perform reliably in both short and long interactions. This approach addresses the unique challenges posed by LLM-based agents, ensuring their outputs meet the high standards required for real-world applications.

###### **Coherence**

Coherence testing ensures that an agent’s outputs remain logical, contextually relevant, and consistent across the span of an interaction. For agents managing multistep workflows or sustaining extended dialogues, coherence is what enables seamless, intuitive exchanges. The agent must retain and appropriately use context—such as user preferences or previous actions—so that its responses build naturally on what has come before. This is especially critical in multiturn conversations, where the agent should reference prior information without prompting the user to repeat themselves.

For instance, in the cracked mug scenario from our running customer support agent example, coherence requires the agent to reference the initial damage report and photo upload when confirming a refund, avoiding lapses such as overlooking the multi-item order details (e.g., only refunding the mug from order_id A89268 while ignoring other items). In more complex cases, like a modification request following a refund (as in modify_2 ), the agent must maintain logical flow by confirming address changes without introducing contradictions in the conversation history.

Testing for coherence involves simulating extended interactions, verifying that the agent maintains a consistent understanding of state, and that its actions follow a logical, goal-directed sequence. Contradictions or lapses—such as conflicting recommendations or overlooked dependencies—are flagged as coherence failures. In customer service, for instance, coherence tests ensure that an agent’s responses logically address user questions and maintain professional, unambiguous communication.

Ultimately, coherence testing is vital for preserving trust, usability, and the practical value of agentic systems in real-world applications. By rigorously evaluating for logical flow, context retention, and contradiction avoidance, developers ensure that agents operate reliably—even as tasks grow in complexity or session length.

###### **Hallucination**

Hallucination in AI systems occurs when an agent generates incorrect, nonsensical, or fabricated information. This challenge is particularly significant in systems designed for knowledge retrieval, decision making, or user interactions, where accuracy and reliability are paramount. Addressing hallucination requires rigorous testing and mitigation strategies to ensure the agent consistently produces responses grounded in reality.

To mitigate this, developers should ground outputs in verifiable data using techniques like retrieval-augmented generation (RAG), which cross-references trusted sources to enhance factual accuracy, as seen in legal AI tools that reduce hallucinations compared with general models.

At its core, mitigating hallucination begins with ensuring content accuracy. This involves verifying that the agent’s outputs are based on factual data rather than fabrications. Systems must be rigorously tested to cross-check their responses against trusted sources of information. For instance, a medical diagnostic agent should base its recommendations on verified clinical guidelines, while a conversational agent providing historical facts must rely on validated databases. Regular audits of the system’s knowledge base and decision-making processes are critical to maintaining this standard of accuracy.

Data dependence is another critical factor in addressing hallucination. The reliability of an agent’s outputs is directly tied to the quality of its data sources. Systems that rely

on outdated, incomplete, or poorly vetted data are more prone to generating erroneous information. Testing processes must ensure that the agent consistently draws from accurate, relevant, and up-to-date sources. For example, an AI summarizing news articles should rely on credible, well-regarded publications and avoid unverified sources.

Feedback mechanisms are essential for detecting and addressing hallucination. These systems monitor the agent’s outputs, flagging inaccuracies for review and correction. Human-in-the-loop feedback loops can be particularly effective, enabling domain experts to refine the system’s responses over time. In dynamic applications, automated feedback mechanisms can identify discrepancies between the agent’s predictions and actual outcomes, triggering updates to models or data sources to improve reliability.

Mitigations for hallucinations have evolved to emphasize hybrid human-AI feedback loops, where domain experts collaborate with AI systems in real-time oversight— such as in crisis self-rescue scenarios—to refine outputs, reduce cognitive load on users, and correct fabrications before they propagate. This approach integrates automated detection with human judgment, enhancing reliability in high-stakes applications like healthcare or legal advice. Additionally, cost-aware evaluations are gaining traction, focusing on balancing hallucination reduction with inference expenses; for instance, frameworks now quantify “hallucination cost” through metrics that weigh accuracy improvements against computational overhead, enabling more efficient deployments without sacrificing performance.

By prioritizing content accuracy, enforcing data dependence, leveraging feedback mechanisms, and rigorously testing for diverse scenarios, developers can minimize the risk of hallucination and build agents that deliver reliable, grounded, and trustworthy outputs. This disciplined approach ensures that the system operates as a reliable partner in its intended domain, meeting user expectations and adhering to high standards of accuracy and integrity.

###### **Handling Unexpected Inputs**

Real-world environments are unpredictable, and agents must be robust in the face of unanticipated, malformed, or even malicious inputs. Integration tests in this area intentionally supply inputs that fall outside the training or design assumptions—such as unexpected data formats, slang or typos in user language, or partial failures of external services. The goal is to ensure that the agent neither crashes nor produces harmful outputs, but instead responds gracefully: by clarifying, declining, or escalating as appropriate.

In the context of our ecommerce agent, unexpected inputs could include malformed order IDs (e.g., a typo in “A89268” during a cracked mug refund) or ambiguous requests blending intents (as in cancel_4_refund , where a cancellation is requested

for a delivered order), requiring the agent to clarify or escalate rather than proceeding with erroneous tool calls like issue_refund . Systematic testing with adversarial variations from our evaluation sets, such as injecting slang or partial failures in photo uploads, ensures graceful handling without leaking sensitive order information.

Effective integration testing covers not only random “fuzzing” of inputs but also systematic exploration of edge cases informed by historical incidents or adversarial analysis. For safety-critical applications, it is important to verify that, even under stress, the agent does not leak sensitive information, violate policy, or cause downstream failures. By continuously extending and refining these tests as the agent evolves, developers can build systems that are robust, trustworthy, and ready for the complexities of the real world.

###### **Preparing for Deployment**

As an agentic system matures, transitioning from development to deployment requires disciplined readiness checks and quality gates to ensure reliability and trustworthiness in production. Production readiness is more than passing tests—it is a holistic assessment of whether the system can perform its intended function safely, consistently, and efficiently in a real-world environment.

Establishing clear deployment criteria is the first step. These often include meeting quantitative performance thresholds on relevant evaluation sets, demonstrating stability under stress and edge cases, and validating that all core workflows behave as intended. In practice, teams should use structured checklists to confirm that all components—tools, planning, memory, learning, and integrations—have been rigorously tested and reviewed. Key criteria may include passing end-to-end integration tests, meeting latency and uptime targets, and verifying the absence of critical or highseverity bugs.

A critical mechanism for enforcing these criteria is the use of gating mechanisms. Gates are automated or manual checks that prevent promotion to production unless all requirements are satisfied. This might involve blocking deployment if any regression is detected on the latest evaluation suite, or requiring explicit approval from technical and product leads after a successful pilot or beta phase. Gates can be configured to escalate issues for human review when automated results are ambiguous.

Equally important is establishing a reliable process for rolling out new versions, monitoring for regressions post-launch, and enabling rapid rollback if unexpected issues arise. This is where the foundation of robust, offline evaluation pays dividends, providing the confidence that the deployed system will perform as expected while minimizing risks to users and the business.

By rigorously preparing for deployment and establishing clear quality gates, teams create a culture of accountability and excellence, ensuring that only agentic systems meeting the highest standards reach users.

###### **Conclusion**

Measurement and validation form the backbone of developing robust and reliable agent-based systems, ensuring they are ready to perform effectively in real-world scenarios. By defining clear objectives and selecting relevant metrics, developers create a structured foundation for assessing an agent’s performance. Thorough error analysis uncovers weaknesses and informs targeted improvements, while multitier evaluations provide a holistic view of the system’s capabilities, from individual components to full-scale user interactions.

As illustrated through our running example of the ecommerce customer support agent—handling everything from a simple cracked mug refund ( order_id A89268 ) to complex cancellations and modifications—these measurement and validation practices ensure robust performance across diverse scenarios. By iteratively refining metrics and evaluation sets based on such threaded cases, teams can deploy agents that not only meet objectives but also adapt to evolving user needs, ultimately fostering trust and efficiency in real-world applications.

This layered and methodical approach ensures that agent-based systems achieve their performance goals, deliver a seamless and satisfying user experience, and maintain reliability even in dynamic and complex environments. Comprehensive unit and integration tests safeguard the integrity of core functionalities and system-wide behaviors, enabling developers to address potential issues before deployment.

Ultimately, diligent measurement and validation empower teams to deploy agent systems with confidence, knowing they can withstand the challenges of real-world operation while meeting user needs. By prioritizing these practices, developers not only enhance the quality and reliability of their systems, but also pave the way for meaningful contributions to their intended applications across diverse industries and use cases.

### **CHAPTER 10 Monitoring in Production**

Whether you’re a product owner, machine learning (ML) engineer, or site reliability engineer (SRE), once agents hit production, you need to see what they’re doing and why. Shipping agentic systems is only the halfway point. The real challenge begins once your agents are operating in dynamic, unpredictable, high-stakes environments. Monitoring is how you learn from reality—how you catch failures before they escalate, identify regressions before users notice, and adapt systems in response to realworld signals.

Unlike traditional software, agents behave probabilistically. They depend on foundation models, chain together tools, and respond to unbounded user inputs. You can’t write exhaustive tests for every scenario. That’s why monitoring becomes the nervous system of your deployed agent infrastructure.

Monitoring isn’t just about detecting problems. It’s the backbone of a tight feedback loop that accelerates learning and iteration. Teams that monitor well learn faster, ship safer, and improve reliability with every deployment.

In this chapter, we focus on open source monitoring. While there are excellent commercial platforms like Arize AX, Langfuse, and WhyLabs, we’ll concentrate here on tooling you can self-host and extend freely. Our reference stack includes:

###### _OpenTelemetry_

For instrumenting agent workflows

###### _Loki_

For log aggregation and search

###### _Tempo_

For distributed traces

###### _Grafana_

For visualization, alerts, and dashboards

We’ll walk through how to integrate each of these with a LangGraph-based agent system, then show how the pieces fit together into a feedback loop that closes the gap between observation and improvement.

###### **Monitoring Is How You Learn**

Understanding root causes of agent failures—from software bugs and foundation model variations to architectural limits—is essential for proactive maintenance and system adaptability. Each type demands targeted detection, analysis, and fixes to maintain stability in production.

The best agent systems improve over time through feedback. Traditional monitoring reacts to crashes or throughput dips, but for agents, it’s foundational: revealing emergent issues in probabilistic behaviors and guiding development amid uncertainty.

Agent failures are subtle—a tool succeeds but cascades errors, an LLM output sounds fluent yet misleads, or a plan partially works but misses the goal. These mismatches rarely crash systems; monitoring must expose them swiftly, making production observability nonoptional.

Failures aren’t just incidents—they’re test cases. Every time an agent breaks in production, that scenario should be captured and turned into a regression test. But the same is true for success: when an agent handles a complex case well, that trace can become a golden path worth preserving. By exporting both failure traces and exemplar successes into your test suite, you create a living CI/CD corpus that reflects realworld conditions. This practice helps “shift left” your monitoring strategy—catching issues earlier in development, and ensuring that new agent versions are continuously validated against the actual complexity of production behavior.

A key challenge in monitoring probabilistic systems like agents is distinguishing true “failures” (systematic issues requiring fixes) from expected variations (inherent nondeterminism where outputs differ but stay acceptable). A simple decision tree can guide this. Start with the output—does it meet success criteria (e.g., eval score > 0.8)? If yes, monitor trends but no action is needed. If no, check reproducibility (rerun 3–5 times; failure rate > 80% indicates systematic bug for engineering review). If it is not reproducible, assess confidence/variance (e.g., LLM score > 0.7, Kullback-Leibler divergence < 0.2 from baseline). Within the bounds means expected variation (log for drift watch), and outside the bounds suggests anomalous failure (e.g., input drift via population stability index > 0.1, triggering mitigation like retraining or guardrails).

This flowchart, applied in tools like Grafana, prevents overreaction to noise while catching real degradations early.

Effective monitoring spans infrastructure signals (latency, error rates, CPU) and semantic behaviors (intent grasp, tool selection, hallucination, task abandonment). Was the user’s intent understood? Was the right tool selected? Did the system produce hallucinated content? Did the user abandon the task halfway through? These are not questions traditional monitoring systems are built to answer, but they are critical to ensuring agents remain trustworthy, helpful, and aligned.

Build a layered feedback loop: instrument runtime events (tool calls, generations, fallbacks) with context, streaming to backends like Loki (logs), Tempo (traces), and Grafana (visualization/alerting). Append evaluation signals—hallucination scores or drift indicators—via external critics in real time.

It’s worth emphasizing that all of this can—and should—be part of the same observability pipeline used for production services. The same Prometheus instance that tracks service health can also track agent success rates. The same Grafana dashboards used by SREs can include semantic error rates, model latency distributions, and tool usage graphs. There is no need for a separate monitoring stack; agents benefit from the same rigor and visibility as any other critical software service.

Of course, observability data often contains sensitive content. Logs may include user messages, tool inputs, or intermediate LLM generations. To maintain compliance and user privacy, teams should configure separate monitoring clusters with strict rolebased access control (RBAC). Sensitive data can be routed to isolated backends with encryption-at-rest and access auditing, ensuring that debugging and performance analysis remain possible without compromising trust or compliance obligations. It’s also common practice to redact, hash, or mask personally identifiable information (PII) from observability logs before export. OpenTelemetry provides hooks for data scrubbing during span export, enabling fine-grained control over what leaves the boundary of the application.

Ultimately, monitoring turns metrics into action—helping teams spot what’s critical and respond fast. The following sections show how open source tools build this loop, accelerating development, robustness, and reliability in live environments.

Before diving into instrumentation details, it’s helpful to define what you actually want to observe. Effective monitoring begins with choosing the right metrics—those that reveal not just whether the system is up, but whether it’s working as intended.

Table 10-1 is a practical taxonomy of metrics, organized by layer of abstraction, that can guide what to collect, visualize, and alert on.

_Table 10-1. Taxonomy of metrics_

Each of these metrics can be logged via OpenTelemetry, aggregated in Prometheus or Loki, visualized in Grafana, and (where appropriate) linked to traces in Tempo. The goal is not to collect everything, but to collect what is necessary to detect meaningful change—and to do so in a way that supports rapid diagnosis and continuous improvement.

###### **Monitoring Stacks**

Selecting the right monitoring is an important decision that can either accelerate or impede the pace of development for your agent system. Observability must capture

not only traditional infrastructure metrics (e.g., latency, uptime) but also semantic insights like hallucination rates, tool efficacy, and distribution shifts in user inputs. The current landscape emphasizes open source tools that integrate seamlessly with frameworks like LangGraph, CrewAI, and AutoGen, supporting distributed tracing, logging, and alerting while handling the probabilistic nature of foundation models. Many companies already have established enterprise plans for managed logging stacks (e.g., Splunk, Datadog, or New Relic), and foundation models or agents don’t necessarily require an entirely new monitoring solution. In most cases, it’s wise to extend your existing stack—leveraging its familiarity, scalability, and integrations— unless you have strong needs for specialized features like evaluations that are native to foundation models or lightweight self-hosting. We’ll explore several equivalent open source options in the following subsections, highlighting features, integrations, and trade-offs to help you choose or adapt based on your environment.

###### **Grafana with OpenTelemetry, Loki, and Tempo**

This stack offers high composability, making it a flexible choice for teams building custom observability around agents:

###### _Setup and integration_

Initialize OpenTelemetry (OTel) in your LangGraph application to export spans (e.g., for tool calls or LLM generations) and metrics (e.g., token usage). The logs route to Loki for structured querying, while traces go to Tempo for end-to-end visibility. Grafana pulls from both, establishing dashboards that correlate agent behavior (e.g., planning latency) with system health. Example: wrap a LangGraph node with OTel spans to track tool_recall metrics, exporting to Tempo for querying failed sessions.

###### _Key features_

The key features are the real-time dashboards for semantic metrics (e.g., hallucination scores via custom plug-ins); alerting on anomalies like retry spikes; and strong community for AI extensions (e.g., 2025 Grafana plug-ins for LLM drift detection). It’s scalable for production, with low overhead when self-hosted.

###### _Trade-offs_

Pros include flexibility (mix-and-match components) and no vendor lock-in; cons are the multitool setup (requires managing Loki/Tempo separately) and a steeper learning curve for noninfra teams. This is ideal for enterprises extending existing infra monitoring to agents.

###### **ELK Stack (Elasticsearch, Logstash/Fluentd, Kibana)**

The ELK Stack is a mature option emphasizing powerful search and analytics, often extended from existing enterprise setups for AI workloads:

###### _Setup and integration_

Use OTel collectors to send agent traces/logs to Elasticsearch (via Logstash for ingestion). Kibana provides the UI for querying and dashboards. For LangGraph, instrument nodes to log structured events (e.g., JSON with tool params), leveraging Elasticsearch’s ML jobs for anomaly detection on agent outputs. Example: query “hallucination events where confidence < 0.7” across sessions, correlating with user feedback.

###### _Key features_

Key features include advanced full-text and vector search for LLM outputs (e.g., embedding-based drift detection); built-in ML for predictive alerts (e.g., forecasting tool failure rates); and scalability for massive log volumes with clustering.

###### _Trade-offs_

The pros are superior search and analytics (e.g., fuzzy matching on prompts, better for long-tail failures) and enterprise-grade scalability. The cons are higher resource demands (Elasticsearch is memory-intensive) and a more complex deployment (multiple services). It is best for teams with existing ELK investments, extending it for agent-specific semantic logging without starting from scratch.

###### **Arize Phoenix**

Phoenix focuses on LLM tracing and evaluation, providing a debug-oriented extension for agent monitoring in existing environments:

###### _Setup and integration_

Use Phoenix’s Python SDK to instrument LangGraph (e.g., trace LLM calls with evals). It supports OTel export for hybrid use. Example: visualize agent traces with auto-scorers for accuracy, exporting to notebooks for analysis.

###### _Key features_

Key features include structured tracing with evals (e.g., RAG quality, hallucination detection); Jupyter integration for ML workflows; and 2025 enhancements for multiagent coordination metrics.

###### _Trade-offs_

The pros are it is specialized for evals/debugging (faster insights on agent quality) and lightweight for prototyping. The con is that it is limited to traces/evals (supplement for full logs/metrics) and more dev-oriented than ops. It is great for research/ML teams adding agent insights to managed enterprise stacks.

###### **SigNoz**

SigNoz is a unified, OTel-native platform that combines metrics, traces, and logs in a single tool, suitable for streamlined extensions of basic monitoring setups:

###### _Setup and integration_

SigNoz ingests OTel data directly, with auto-instrumentation for Python (e.g., LangGraph). Add spans for agent steps (e.g., planning latency) and query via its UI. Example: trace a multistep agent flow, filtering by token_usage > 1000 to spot inefficiencies, with built-in evals for LLM quality.

###### _Key features_

It has integrated AI-powered insights (e.g., anomaly detection on agent traces); custom dashboards for LLM metrics (e.g., prompt drift); and lightweight selfhosting with ClickHouse backend for efficiency.

###### _Trade-offs_

The pros include a simpler setup (single app), lower overhead for small teams, and strong OTel support with AI extensions (e.g., 2025 updates for hallucination auto-scoring). The cons are that it has a less extensible ecosystem (fewer plugins) and that visualization is functional but not as advanced. It is well suited for startups or ML-focused teams extending lightweight monitoring without heavy infra additions.

###### **Langfuse**

Langfuse specializes in foundation model and agent observability, making it easy to extend existing stacks with semantic-focused tracing for agents:

###### _Setup and integration_

Integrate via SDK in LangGraph (e.g., wrap nodes with Langfuse tracers). It captures prompts, outputs, and evals (e.g., custom scorers for coherence). Example: log a full agent session, auto-evaluate for hallucination, and export traces for regression testing.

###### _Key features_

It has LLM-native metrics (e.g., token cost tracking, A/B testing for prompts); session replay for debugging; and it is self-hostable with database backends like PostgreSQL.

###### _Trade-offs_

The pros are that it is tailored for agents/LLMs (as built-in evals save custom work) and easy for dev teams (focus on app-level insights). The cons are that it has a narrower scope (weaker on infra metrics like CPU; pair with Prometheus) and it is less scalable for non-LLM telemetry. It is ideal for extending enterprise logging with agent-specific features without overhauling the core stack.

###### **Choosing the Right Stack**

All these open source stacks are viable equivalents—start by assessing your current setup. If you have an enterprise-managed solution, extend it with OTel instrumentation for agent signals unless you need LLM-specific features like auto-evals (favor Langfuse/Phoenix) or advanced search (ELK). For greenfield projects, Grafana or SigNoz offer broad coverage. Evaluate based on team expertise, data volume, and integration needs—many can hybridize (e.g., OTel to multiple backends). Table 10-2 shows these trade-offs at a glance.

_Table 10-2. Comparison of monitoring and observability stacks_

While the observability landscape offers multiple strong options—each with unique strengths in scalability, ease of use, or LLM-specific features—this competition drives innovation and ensures teams can find a fit for their needs, whether extending enterprise stacks or starting fresh. For our examples in the following sections, we’ll focus on OTel with Grafana, Loki, and Tempo, as it provides a highly composable, open source foundation that’s widely adopted and integrates seamlessly with agent frameworks like LangGraph, enabling us to demonstrate core concepts without vendor lock-in. With a stack selected, the next step is instrumentation—embedding telemetry directly into your agent runtime to capture meaningful signals, as explored in the next section.

###### **OTel Instrumentation**

The first step in building an effective monitoring loop is instrumentation. Without high-quality signals embedded directly into your agent runtime, you’re flying blind. OTel provides the foundation for structured, interoperable telemetry across traces, metrics, and logs—and it integrates well with LangGraph-based agent systems.

LangGraph is structured as a graph of asynchronous function calls. Each node in the graph represents a functional step in an agent workflow—perhaps planning, calling a tool, or generating a response with an LLM. Because each step is already isolated and explicitly declared, it’s straightforward to instrument each one with OTel spans. These spans create a structured trace that records not just when steps started and ended, but what they were trying to do and how they performed.

For each node, we recommend starting a span at the beginning of the function and annotating it with relevant metadata. For example, in a tool-calling node, you might capture the tool name, the specific method called, the latency of the response, the success or failure status, and any known error codes. In nodes where the LLM generates output, the span can include prompt identifiers, token counts, model latency, and flags for hallucination risk or confidence scores.

This instrumentation does not require major architectural changes. OTel’s Python SDK can be initialized once at startup, and spans can be created and closed using simple context managers. The distributed tracing context is automatically propagated across async calls, making it easy to correlate end-to-end behavior even in complex, branched agent flows. Here is a simplified example of how to wrap a LangGraph node with a trace span:

Spans can include events (like fallback triggers or retries), nested subspans (to measure downstream API calls), and exception capture for automatic error tagging. These traces are exported in real time to backends like Tempo or Jaeger and visualized alongside logs and metrics in Grafana.

In addition to traces, OTel can emit structured logs and runtime metrics. For example, you can record the number of times a specific tool is invoked, the average response time per planning node, or the percentage of failed tasks per model version. These metrics are invaluable for creating dashboards and alerts that track long-term performance and detect early signs of degradation.

Instrumentation must be thoughtfully scoped. Too much detail becomes noisy; too little makes root cause analysis difficult. The key is to attach just enough context at each step—user request IDs, session metadata, agent configuration state, skill names, and evaluation signals—so that when something goes wrong, the trail of evidence is coherent, complete, and easily searchable.

Tempo acts as the trace backend. Every span you instrument in LangGraph—each tool call, plan generation, or fallback—is part of a distributed trace. Tempo stores these traces in a highly scalable fashion and supports deep querying. For instance, you can filter all traces where the planning step took longer than 1.5 seconds, or

where a particular tool call failed with a given error code. This enables precise debugging of subtle issues that emerge only under real-world, multistep execution conditions.

Loki, by contrast, serves as your log aggregation layer. It captures structured logs— often in JSON format—from across your agent infrastructure. Each LangGraph node can emit structured log events during its execution: when a user query is received, when a tool is invoked, when an LLM produces an ambiguous response, or when a fallback path is triggered. Logs can be annotated with span and trace IDs, making it easy to correlate logs and traces from the same user session or agent workflow. While Loki is a great fit for structured logs, teams requiring full-text search, role-based views, or higher ingestion throughput may also consider Elasticsearch or commercial options like Datadog logs or Honeycomb.

Grafana unifies both of these data streams into a single pane of glass. It provides the visualization layer where logs from Loki and traces from Tempo can be explored side by side. Within Grafana, you can construct dashboards that show live trace data, drill down into individual requests, and correlate structured logs with performance metrics. You can also build custom alerting rules—for example, flagging when error rates for a particular agent spike above a threshold, or when tool response latency crosses a defined boundary.

Together, OTel, Tempo, Loki, and Grafana form a complete, open source observability stack for agent systems. They enable deep inspection of behavior, fast root cause analysis, historical trend evaluation, and proactive anomaly detection. This integration is what transforms raw telemetry into operational intelligence—and operational intelligence into a development accelerant. This observability enables real-time debugging, trend analysis, and continuous learning—all of which are essential to the safe and scalable deployment of intelligent agents in production.

###### **Visualization and Alerting**

Once your LangGraph agents are instrumented with OTel and streaming logs and traces into Loki and Tempo, the final and most impactful layer is visualization and alerting—made possible with Grafana. Grafana is more than just a dashboarding tool; it’s the operational frontend for observability, where signals become stories and metrics become actions.

Grafana connects seamlessly with Loki and Tempo as native data sources. For traces, Grafana’s Tempo integration enables you to browse full execution traces for individual agent runs. This includes viewing span hierarchies that represent the sequence and timing of steps an agent took—from receiving a user query to selecting a plan, calling tools, and composing the final output. You can filter traces by latency, status, span name, or any custom attribute you’ve attached in your LangGraph nodes. This is

invaluable for debugging multistep agent behaviors, especially when performance degrades or edge-case bugs arise.

For logs, the Loki plug-in enables querying structured log events emitted during agent execution. Grafana’s log panels enable you to visualize real-time logs across all agents; filter by agent name, user session, error type, or trace ID; and correlate logs with related traces. Because logs and traces share common metadata—such as request or session IDs—Grafana lets you jump directly from a spike in log volume or error messages to the exact trace that triggered them.

But Grafana’s true power lies in building dashboards tailored to your agents’ semantics and success criteria. a GenAI Observability dashboard can display key metrics like request rates, usage costs, token consumption, and request distributions for foundation models and vector databases. For example, you might build a dashboard showing the following:

- Token usage per agent per hour (to detect model verbosity regressions)

- P95 latency for tool calls and planning nodes

- Task success rate by workflow or prompt template version

- Fallback frequency by tool or skill

- Drift indicators based on embedding similarity of user queries over time

Each of these panels not only helps visualize system performance but also guides ongoing development. If a particular tool starts failing more often, or if token usage increases unexpectedly, these signals help prioritize debugging and optimization.

Grafana also supports custom alerts. You can define thresholds on any metric and trigger alerts via Slack, email, PagerDuty, or any other integration. For example, you might trigger alerts in the following circumstances:

- Hallucination rates exceed 5% in the last 30 minutes

- Retry loops occur more than three times in a single session

- Average response time for a critical tool increases by more than 50%

Alerts ensure your team is aware of regressions and anomalies in real time, even if no one is actively watching the dashboard. Combined with Loki logs and Tempo traces, these alerts help close the feedback loop rapidly.

Grafana’s alerting system is highly extensible, integrating seamlessly with popular incident management tools like PagerDuty for escalating notifications to on-call teams—ensuring that high-severity issues, such as sudden spikes in hallucination rates or task failures, trigger structured response workflows with automated paging and acknowledgment. For more specialized error monitoring, Sentry can be layered in to capture and analyze exceptions within agent code, providing stack traces, breadcrumbs, and release health metrics that complement Grafana’s dashboards; this is particularly useful for debugging probabilistic bugs in foundation model calls or tool invocations, with Sentry’s SDK easily instrumented alongside OTel.

For teams seeking an all-in-one solution tailored to agentic systems, platforms like AgentOps.ai offer a streamlined alternative, combining tracing, metrics, evaluations, and alerting in a single package optimized for foundation models and agents. AgentOps.ai handles semantic monitoring (e.g., auto-scoring outputs for quality) and integrates with existing stacks, reducing setup overhead compared with composing Grafana components—though it may introduce vendor dependency. These options create flexibility: extend Grafana with PagerDuty/Sentry for robust alerting, or adopt AgentOps.ai for faster agent-specific insights, depending on your operational maturity and focus.

By integrating Grafana deeply into your agent development lifecycle, you create a living interface to your deployed systems. It becomes the shared canvas where product teams, engineers, and reliability staff can observe, debug, iterate, and improve. In the world of agent-based systems—where bugs are probabilistic and failure modes are emergent—this kind of unified visibility isn’t just nice to have. It’s essential.

###### **Monitoring Patterns**

Once an observability stack is in place—spanning instrumentation, logs, traces, dashboards, and alerts—the question becomes: how do we safely ship changes to agentic systems that are inherently probabilistic, adaptive, and hard to predict fully? The answer lies in adopting monitoring-aware development patterns that de-risk experimentation and create safety nets around production changes. In this section, we explore several key patterns that teams can adopt to ensure their agents continue to evolve safely and responsively.

###### **Shadow Mode**

In shadow mode, a new or experimental version of an agent runs alongside the current production agent, processing the same inputs but without serving its outputs to users. This enables developers to log and trace the behavior of the new agent in realworld conditions without affecting user experience.

With OTel, you can instrument both the production and shadow agents and attach a shared request ID. Logs and traces from the shadow agent can then be labeled accordingly in Loki and Tempo, making it easy to compare behavior. You might look at differences in tool selection, latency, token usage, or hallucination frequency. These comparisons are especially useful when trialing new model versions, planning strategies, or prompting techniques.

Shadow mode enables safer innovation. It enables teams to answer: does the new agent do better or worse on live traffic? What breaks? What improves? And it lets you collect this data continuously, in parallel with normal operation.

###### **Canary Deployments**

Where shadow mode gathers information without exposure, canarying goes one step further. A canary deployment serves a new agent version to a small subset of real users—say, 1% or 5% of traffic—while the majority of users continue to interact with the baseline version.

Grafana dashboards are critical in this setup. By filtering all metrics and traces by version tag, you can directly compare success rates, latency, tool usage, and error counts between canary and baseline agents. Alerts can be configured to trigger if the canary shows significant regressions or anomalies.

If the canary behaves well, the deployment can be gradually expanded. If not, it can be rolled back immediately with minimal user impact. Canarying provides the operational safety needed to iterate quickly in production environments.

###### **Regression Trace Collection**

Every time an agent fails in production—whether through hallucination, planning error, or tool misuse—it creates an opportunity for learning. By automatically exporting these failure traces (from Tempo) or log snapshots (from Loki) into your test suite, you build a continuously updated regression corpus.

This turns production failures into training signals. A failed tool call or misaligned output becomes a new test case. Once a fix is implemented, rerunning this trace should pass. Over time, this strategy strengthens your evaluation set with real-world edge cases and helps prevent recurrence of the same failure modes.

###### **Self-Healing Agents**

Finally, monitoring can do more than detect failure—it can help agents recover from it. Agents that are designed to read their own telemetry in real time can implement fallback mechanisms when issues are detected.

For example, if a tool call fails repeatedly, the agent might reroute to a simpler fallback plan or ask the user for clarification. If latency spikes, the agent could skip optional reasoning steps. If hallucination scores are high, it could issue a disclaimer or defer to human review.

These self-healing behaviors are most effective when supported by detailed monitoring data. Each fallback decision can be logged and traced, enabling teams to analyze when and why fallbacks were triggered, and whether they helped resolve the issue.

###### **User Feedback as an Observability Signal**

While much of this chapter has focused on logs, traces, and metrics, user feedback offers a complementary lens—direct insight into how well the agent is meeting human expectations. Feedback can be implicit, such as users rephrasing their inputs, abandoning tasks, or hesitating during interactions. It can also be explicit, like a thumbs-down icon, a star rating, or a free-text comment. Both forms provide realtime signals that can and should be integrated into your monitoring stack.

In practice, implicit feedback metrics—such as task abandonment rate or requery frequency—can be logged and aggregated in Loki and visualized in Grafana just like any other performance metric. They offer early indicators of friction or confusion. Explicit feedback events, like low ratings, can be tied to specific traces in Tempo and trigger alerts when dissatisfaction spikes. Dashboards that combine user sentiment metrics with trace-based technical data enable teams to correlate performance issues with user frustration, giving a fuller picture of agent health.

Critically, user feedback can also drive improvement loops. For example, traces associated with low user ratings can be exported directly to the evaluation set for post hoc

review. If multiple users abandon a specific flow, it may warrant revisiting the planning strategy or retraining the foundation model prompt. By integrating user signals into the broader observability and action framework, teams ensure their monitoring practices remain not only operationally effective but also user-centered.

###### **Distribution Shifts**

One of the subtler, yet most critical, challenges in monitoring agent-based systems is identifying and managing distribution shifts. These occur when the statistical properties of the agent’s environment change over time—whether through evolving user language, new product terminology, changes in API responses, or even updates to the foundation model itself. While such shifts may not trigger explicit errors, they often manifest as degraded performance, misaligned outputs, or increased fallback usage.

Monitoring systems are your first line of defense against this kind of slow drift. Dashboards that track task success rates, tool invocation failures, and semantic metrics— such as token usage trends or hallucination frequency—can surface early signals. For quantitative detection, employ statistical tests like the Kolmogorov-Smirnov (KS) test to compare distributions of input features or outputs. The KS test is a nonparametric statistical test that compares the empirical cumulative distribution functions of two datasets to determine if they are drawn from the same underlying distribution, making it ideal for detecting shifts in continuous features like query lengths, latencies, or numerical metrics without assuming normality. It calculates the maximum vertical distance (KS statistic) between the distributions, along with a _p_ -value for statistical significance; thresholds like KS > 0.1 (often paired with _p_ -value < 0.05) indicate meaningful divergence, triggering alerts for potential drift in agent inputs or outputs. In this code, SciPy’s ks_2samp function is applied to sample arrays of historical and current data, printing a detection message if the statistic exceeds the threshold. Here’s a small Python example using SciPy to detect drift in query lengths:

Kullback-Leibler (KL) divergence measures how one probability distribution diverges from another, often used to detect concept drift by quantifying shifts in token distributions (e.g., changes in word frequencies that might indicate evolving user language or new terminology). It is not symmetric KL(P||Q) ≠ KL(Q||P) and can signal when current data (Q) deviates significantly from historical baselines (P), with higher

values indicating greater drift—e.g., a threshold > 0.5 might flag concept changes in embeddings. In this code, we normalize frequency vectors to probabilities, add a small epsilon to avoid log(0) errors, and compute the sum of _P * log(P/Q)_ ; the example assumes simplified token count arrays for historical and current data:

The population stability index (PSI) is a metric for detecting shifts in categorical or binned continuous variables (e.g., tool usage categories like “refund,” “cancel,” “modify”) by comparing percentage distributions between historical and current datasets, often divided into buckets for granular analysis. It sums natural_logarithm(actual_percent / expected_percent) across categories, where low PSI (< 0.1) means stability, 0.1–0.25 indicates minor drift (monitor), and > 0.25 signals major drift (intervene—e.g., retrain). This helps flag changes in patterns without assuming normality, making it suitable for agent metrics like invocation frequencies:

Sudden drops in accuracy (e.g., > 5–10% over a rolling 24-hour window), increases in task abandonment (> 15%), or surges in retries (> 20% session rate) are all potential indicators of input or concept drift. Embedding-based techniques, such as computing cosine similarity between current and historical query vectors, can also be used to compare new inputs against baselines (e.g., mean similarity < 0.8 triggers review), often implemented via libraries like Evidently AI for automated alerting in Grafana.

Responding to these shifts is part of building resilient systems. Transient changes may be addressed by tuning thresholds or updating parsing logic, while persistent shifts might require retraining workflows or adapting to new APIs. Feedback loops, such as logging and exporting degraded traces for analysis, help teams determine whether issues are temporary or systemic. As always, response strategies benefit from the realtime visibility provided by a strong observability stack—enabling teams to act before drift becomes failure. Responding to these shifts is part of building resilient systems. Transient changes may be addressed by tuning thresholds or updating parsing logic, while persistent shifts might require retraining workflows or adapting to new APIs— guided by drift severity from the statistical measures (e.g., prioritize retraining if PSI > 0.25 persists over 48 hours). Feedback loops, such as logging and exporting degraded traces for analysis, help teams determine whether issues are temporary or systemic—perhaps via A/B testing post-detection to validate fixes. As always, response strategies benefit from the real-time visibility provided by a strong observability stack—enabling teams to act before drift becomes failure.

###### **Metric Ownership and Cross-Functional Governance**

As teams deploy agent-based systems, a subtle but serious organizational challenge emerges: who owns which metrics? In traditional software stacks, there’s a clear split: infrastructure teams own latency and uptime, product teams own conversion or user success, and ML teams (if present) build models, and manage the health and performance of them, with responsibility for both the engineering and product implications. But agents powered by foundation models don’t respect these boundaries—and neither should your monitoring strategy.

A foundation model response isn’t just a model artifact—it’s the product. A long chain of tool calls, retries, fallbacks, and generation steps isn’t a backend quirk—it’s the user experience. And a five-second plan generation delay isn’t a model limitation—it’s often a prompt or workflow design decision that someone made on the product team.

That’s why logs, traces, and evaluation signals from agents belong in the core observability platform, alongside service health and system metrics. If product dashboards and model notebooks are the only place that agent metrics show up, you’re missing the full picture—and likely masking systemic issues.

Latency is a perfect example. Teams often adopt the mindset that “foundation models are slow,” and then inadvertently build latency into everything—from verbose prompts to unnecessary retries to bloated plans. Without rigorous, trace-based instrumentation, this drift goes undetected. Before long, the whole system feels sluggish—not because the infrastructure is underpowered, but because the product and ML teams normalized delay as inevitable.

The solution isn’t to offload latency ownership to infra or UX to product. It’s to build shared dashboards where teams can do the following:

- Product leads can see how planning latency and fallback rate correlate with task abandonment.

- ML engineers can monitor hallucination rates and drift alongside user feedback.

- Infra/SRE teams can alert on token spikes and tool flakiness that affect system reliability.

Each team must own part of the agent telemetry—and no one team can interpret it in isolation. To address the organizational challenges of metric ownership, teams can use a Responsibility Assignment Matrix (RACI chart) to clarify roles across functions. In a RACI chart, each task or metric is assigned one or more of the following: R (Responsible: does the work), A (Accountable: owns the outcome), C (Consulted: provides input), or I (Informed: kept updated).

Table 10-3 is a template tailored to agent monitoring, which you can adapt based on your team’s structure, size, and specific metrics. This promotes cross-functional collaboration by ensuring no metric falls through the cracks while avoiding silos.

_Table 10-3. RACI matrix of monitoring metrics and cross-functional responsibilities_

A trace that shows a tool being called four times in a loop, followed by a long generation, a vague response, and user abandonment—that’s not just an engineering detail. That’s a product failure. And it’s only visible when logs and spans are routed through a shared platform like Loki and Tempo, not hidden in disconnected metrics tabs.

To make this work, use the following practice:

- Use shared observability dashboards with version tags and semantic metrics. Highly effective teams don’t debate which dashboard is more accurate—they work across functional boundaries to improve the experience for customers together.

- Tag spans and logs with product context (feature flag, user tier, workflow ID).

- Create cross-functional triage rituals, where product, infra, and ML review telemetry together—especially after launches or major regressions.

- Avoid double standards: don’t hold foundation model latency to a different bar than other services. Slowness that impacts users is everyone’s problem.

Agentic systems demand cross-functional observability. The monitoring stack isn’t just for detecting outages—it’s the interface through which engineering, ML, and product learn to speak the same language about what the system is doing, how well it’s performing, and where it needs to evolve.

###### **Conclusion**

Monitoring agent-based systems is more than a safety check—it is the discipline that enables intelligent systems to thrive in real-world environments. In this chapter, we’ve seen that monitoring is not just reactive; it is how teams learn from production, adapt to change, and accelerate progress.

From foundational instrumentation with OpenTelemetry, to real-time log and trace collection via Loki and Tempo, to dashboards and alerts in Grafana, we outlined how to build an open source feedback loop that surfaces issues before they become outages—and turns every deployment into an opportunity for refinement.

We explored practical techniques like shadow mode, canarying, fallback logging, and user sentiment tracking. We emphasized not only what to measure but also how to act. And we showed how monitoring helps detect not just failures but slow drifts in context, data, or behavior that can quietly undermine performance if left unchecked.

The path forward is clear: teams that build agent systems with observability in mind—who instrument, visualize, and learn from their agents in flight—gain a powerful edge. They iterate faster. They trust their metrics. They recover gracefully when things go wrong.

In a world where agentic systems are becoming core infrastructure, robust monitoring isn’t optional—it’s foundational. And those who master it will lead the way in creating intelligent, resilient, and trustworthy agents at scale.

### **CHAPTER 11 Improvement Loops**

In any sufficiently complex multiagent system, failure is not an anomaly—it’s an inevitability. These systems operate in dynamic, real-world environments, interacting with diverse users, unpredictable inputs, and rapidly changing external data sources. Even the most well-designed systems will encounter edge cases, ambiguous instructions, and emergent behaviors that the original design didn’t anticipate. But the real test of a system isn’t whether it fails—it’s how well it learns from those failures and improves over time. This chapter focuses on building feedback-driven improvement loops that enable agent systems to not only recover from failure but to evolve and refine themselves continuously.

Continuous improvement is not a single mechanism but an interconnected cycle of using feedback pipelines to aid in diagnosing issues, running experiments, and learning. First, failures must be observed, understood, and categorized through feedback pipelines that surface actionable insights. These pipelines combine automated analysis at scale with human-in-the-loop review to extract meaningful conclusions from raw telemetry data and real-world user interactions. Next, proposed improvements must be validated in controlled environments through experimentation frameworks like shadow deployments, A/B testing, and Bayesian Bandits. These techniques provide structured pathways for rolling out changes incrementally, minimizing risk while maximizing impact. Finally, improvements must be embedded into the system through continuous learning mechanisms, whether through immediate in-context adjustments or periodic offline retraining. To understand this cycle of continuous improvement, it’s helpful to draw an analogy from reinforcement learning, where agents learn optimal behaviors through iterative interactions with their environment. See.

Many teams rely on pretrained foundation models without directly training their agents—and often lack structured improvement loops altogether. This chapter explores how to close that gap by implementing feedback-driven mechanisms that enable agents to adapt and refine over time based on real-world interactions with their environment. Fine-tuning, as we discussed in Chapter 7, is an effective way to close this loop, but in this chapter, we’ll discuss a wider range of techniques beyond fine-tuning.

However, improvement is not purely a technical challenge—it’s also an organizational one. Effective improvement loops require alignment across engineering, data science, product management, and UX teams. They require systems for documenting insights, prioritizing improvements, and safeguarding against unintended consequences. Most importantly, they require a culture of curiosity and iteration—one that sees every failure as a valuable source of information and every success as a foundation for further refinement.

This chapter breaks down continuous improvement into three core sections. The first section explores the architecture of feedback pipelines, detailing how to collect, analyze, and prioritize insights from both automated tools and human reviewers. Next, I’ll delve into experimentation frameworks, explaining how techniques like shadow deployments and A/B testing can validate proposed changes in low-risk environments. Then I’ll cover continuous learning, showing how systems can adapt dynamically through in-context strategies and periodic offline updates. Table 11-1 provides an overview of what we’ll cover.

_Table 11-1. Improvement loop methodologies_

In the end, building a system that improves itself isn’t just about fixing what’s broken—it’s about designing a workflow where every failure, insight, and experiment becomes fuel for growth. This chapter provides the tools, strategies, and mindset required to ensure that agent systems adapt to changing circumstances.

###### **Feedback Pipelines**

Automated feedback pipelines are essential for handling the immense volume and complexity of data generated by multiagent systems operating at scale. These pipelines serve as the first line of analysis, continuously monitoring interactions, detecting failure patterns, and clustering issues to surface actionable insights. By leveraging optimization frameworks like DSPy (Declarative Self-Improving Language Programs), Microsoft’s Trace, and Automatic Prompt Optimization (APO), alongside observability tools, these systems can operate with fine-grained visibility into agent behavior, tool usage, and decision-making pathways while enabling automated refinements.

The core function of automated feedback pipelines is to systematically identify recurring issues across agent workflows. For example, repeated failures in skill selection might indicate a misalignment between user intent and the agent’s reasoning process, while consistent errors in tool execution might reveal ambiguities in how tool parameters are being generated. Automated systems excel at pattern recognition across vast datasets, clustering similar failure cases together to make trends apparent and actionable. Instead of relying on engineers to comb through raw logs and traces, automated

pipelines distill these patterns into digestible insights, flagging high-impact issues for immediate attention.

. In this process, an initial prompt is fed into a target model, which generates outputs evaluated against a dataset by an evaluation model. The resulting scores inform an optimization model, which iteratively refines and proposes new prompts to improve performance. This approach enables continuous, data-driven enhancements without manual intervention, making it a cornerstone of scalable feedback pipelines in agentic workflows.

Automated feedback pipelines, powered by tools like DSPy, Trace, and APO, transform raw observational data into iterative improvements, ensuring that multiagent systems remain robust and adaptive. We’ll now discuss several of these approaches in more depth. DSPy is an open source Python framework developed by researchers at Stanford NLP for automatically optimizing and improving systems using foundation models. Unlike traditional prompt engineering, which relies on manual trial and error, DSPy treats language model (LM) pipelines as modular, declarative programs that can be systematically refined using data. Developers define “signatures” (input/ output specifications for tasks), compose them into modules (e.g., chain of thought or ReAct for reasoning and tool use), and apply optimizers (like BootstrapFewshot or MIPROv2) to automatically generate better prompts and few-shot examples and even fine-tune model behaviors based on a dataset of examples and a metric (e.g., exact match or semantic similarity). This data-driven approach enables self-improving loops, where insights from failure patterns are backpropagated to enhance prompts, tools, or reasoning strategies—ideal for proactive optimization in agentic systems.

DSPy integrates with popular LM APIs (e.g., OpenAI, Anthropic) and supports multistage compilation for complex workflows.

Complementing DSPy, Microsoft’s Trace is an open source framework for generative optimization of AI systems. It enables end-to-end training and refinement of AI agents using general feedback signals (e.g., scores, natural language critiques, or pairwise preferences) rather than requiring gradients or differentiable objectives. By treating optimization as a generative process, Trace uses a foundation model to propose and evaluate improvements iteratively, making it suitable for black box systems where traditional methods fall short. This is particularly useful for refining agent behaviors in dynamic, multistep environments, such as incorporating feedback from clustered errors to evolve reasoning strategies or tool invocations over time.

To illustrate the concepts in this section, we’ll use a running example of a Security Operations Center (SOC) analyst agent built with LangGraph. This agent handles cybersecurity tasks like investigating threats, analyzing logs, and triaging incidents. Its core components include a system prompt guiding the agent’s methodology, tools for actions like querying logs or isolating hosts, and a workflow that invokes a foundation model (e.g., GPT-5) bound to those tools. Here’s a simplified excerpt of the agent’s system prompt and a tool definition:

- Threat intelligence analysis and IOC research

- Security log analysis and correlation across multiple systems

- Incident triage and classification (true positive/false positive)

- Malware analysis and threat hunting

- Network security monitoring and anomaly detection

- Incident containment and response coordination

- SIEM/SOAR platform operations

- 1) Analyze security alerts and gather initial indicators

- 2) Use lookup_threat_intel to research IPs, hashes, URLs, and domains

- 3) Use query_logs to search relevant log sources for evidence

- 4) Use triage_incident to classify findings as true/false positives

- 5) Use isolate_host when containment is needed to prevent spread

- 6) Follow up with send_analyst_response to document findings

Our agent has several tools defined here:

In a real deployment, this agent processes alerts like “Suspicious login attempt from IP 203.0.113.45.” Over time, as threats evolve (e.g., new attack vectors emerge), user queries shift, or external data sources change, the agent may encounter failures—such as misinterpreting queries, selecting suboptimal tools, or generating inaccurate triages. This is where feedback pipelines come in: they detect these issues, analyze root

causes, and drive refinements. For instance, “drift” might occur if the agent’s prompt assumes outdated threat patterns (e.g., focusing on IP-based logins when attackers shift to credential stuffing), leading to repeated false negatives. Human engineers can fix this by refining prompts to include updated examples or adding validation steps in tools.

Automated feedback pipelines are essential for handling the immense volume and complexity of data generated by multiagent systems operating at scale. These pipelines serve as the first line of analysis, continuously monitoring interactions, detecting failure patterns, and clustering issues to surface actionable insights. By leveraging observability tools like Trace, DSPy, and similar frameworks, these systems can operate with fine-grained visibility into agent behavior, tool usage, and decision-making pathways.

One of the most powerful capabilities of modern feedback tools is their ability to back-propagate text-based feedback directly into the system’s prompts, skill parameters, and reasoning strategies. For example, if analysis reveals that certain task instructions frequently lead to ambiguous outputs, the pipeline can suggest refinements to the relevant prompts—tightening wording, adjusting constraints, or reordering steps in the reasoning process. Similarly, if tool invocations repeatedly fail due to malformed parameters, automated systems can recommend adjustments to how those parameters are constructed, including introducing validation steps or dynamic fallbacks.

Beyond reactive improvements, automated pipelines also support proactive optimization. By continually analyzing incoming data, they can surface areas of latent risk before they manifest as critical failures. For example, early detection of drift in user query patterns can trigger prompt adjustments to ensure agents remain aligned with evolving user expectations. These proactive insights enable teams to address potential issues before they cascade into larger problems.

However, automated pipelines are not infallible. While they excel at identifying patterns and proposing changes, they cannot fully account for contextual nuances or prioritize improvements based on broader strategic goals. This is where human oversight becomes crucial—engineers must review, validate, and, when necessary, override the recommendations made by these systems. Automated pipelines, therefore, serve not as replacements for human insight but as powerful amplifiers, enabling engineers to focus their expertise where it matters most.

In essence, automated feedback pipelines create a scalable, self-improving loop: they observe, cluster, analyze, and propose improvements across prompts, tools, and reasoning flows. By efficiently managing failure data and generating actionable insights, these systems form the foundation of a robust feedback-driven development cycle, empowering multiagent systems to adapt and evolve continuously in response to realworld demands.

###### **Automated Issue Detection and Root Cause Analysis**

As agentic systems grow in complexity, manual monitoring and debugging quickly become unscalable. Automated issue detection and root cause analysis (RCA) are essential for identifying and diagnosing problems at speed and scale.

In our SOC agent example, imagine the system processes hundreds of alerts daily. Automated detection could flag a spike in failed query_logs calls where the query parameter is malformed (e.g., due to the agent generating overly complex SQL-like queries that the backend can’t parse). Using tools like Trace, the pipeline logs each invocation, clusters similar errors (e.g., “invalid query syntax”), and correlates them with upstream reasoning steps in the agent’s prompt.

Automated issue detection leverages a combination of rule-based triggers, anomaly detection algorithms, and statistical clustering to sift through massive volumes of logs and events. These systems can flag certain patterns:

- Repeated failures in a particular skill or tool

- Sudden spikes in error rates or response times

- Anomalies in user engagement or satisfaction metrics

- Divergent behavior across agent versions or deployment environments

Modern feedback pipelines often employ ML or statistical techniques to detect subtle trends that might otherwise go unnoticed—such as gradual drift in agent decision patterns, or correlations between specific user inputs and downstream failures.

Once an issue is detected, RCA seeks to answer not just _what_ failed, but _why_ . RCA is more than postmortem debugging; it is an ongoing, iterative inquiry into the relationships between user intent, agent reasoning, system architecture, and the external environment. Effective RCA typically follows several steps:

###### _Workflow tracing_

Reconstruct the end-to-end chain of agent decisions, tool invocations, and user interactions leading up to the failure.

###### _Fault localization_

Isolate the precise component—such as a misinterpreted prompt, an inappropriate skill selection, or a tool with restrictive parameter logic—responsible for the breakdown.

###### _Pattern recognition_

Identify whether the failure is an isolated incident or part of a recurring trend, potentially linked to specific user cohorts, data inputs, or system states.

###### _Impact assessment_

Evaluate the frequency and severity of the issue to prioritize response.

Critically, RCA in agentic systems often reveals that failures are not purely technical—they may stem from ambiguous task definitions, gaps in training data, or evolving user expectations that the system was not designed to handle. In some cases, RCA uncovers organizational blind spots, such as success metrics that incentivize the wrong behaviors or workflows that no longer match user needs.

Actionable RCA does more than assign blame; it surfaces opportunities for meaningful system improvement—whether through prompt or tool refinement, skill orchestration changes, or even rethinking the way user needs are represented and communicated.

A robust feedback pipeline, anchored by automated issue detection and RCA, shifts teams from endless triage to a disciplined, insight-driven process where every failure is mined for learning. It is the first step in turning telemetry into transformation— laying the groundwork for all subsequent cycles of experimentation and continuous learning in agentic systems.

###### **Human-in-the-Loop Review**

While automated systems excel at flagging anomalies and surfacing recurring patterns in multiagent workflows, there remain many situations where automated analysis alone is insufficient. Some issues—particularly those involving ambiguous user intent, ethical nuances, conflicting goals, or novel edge cases—require human intuition, domain expertise, and contextual judgment. Human-in-the-loop (HITL) review serves as a critical complement to automated detection and RCA, ensuring that feedback pipelines remain effective, comprehensive, and aligned with broader organizational goals.

For the SOC agent, HITL might escalate cases where automated RCA flags ambiguous triages (e.g., a “suspicious login” that could be a false positive from a virtual private network or a real breach). A security engineer reviews the trace, validates the prompt’s interpretation, and decides on fixes like adding ethical guidelines to the prompt (e.g., “Avoid isolating hosts without confirming impact on critical operations”).

. These candidates undergo review by a human evaluator, who provides manual feedback to refine or approve them, resulting in human-approved outputs delivered to end users. System feedback from the review process loops back to enhance the agent’s performance, ensuring alignment with complex requirements that automation alone cannot handle. This structure

highlights the integration of human judgment to address ambiguities and high-stakes decisions, as seen in the SOC agent’s escalation for nuanced threat assessments.

HITL review is not just a safety net for automation; it is a structured escalation process that brings human judgment to bear on the most complex, ambiguous, or highimpact system issues. Automated pipelines flag incidents that exceed predefined thresholds, exhibit unexplained patterns, or present unresolved conflicts—these are then routed for human evaluation. Escalation criteria may include:

- Persistent errors with no clear technical explanation

- Anomalies in workflows with regulatory or ethical implications

- Failures in high-value or mission-critical tasks

- Conflicting recommendations or diagnoses from automated tools

To find the right balance between human and AI decision making—ensuring humans focus on high-value interventions without being overwhelmed—escalation should prioritize cases with the least model certainty or the most consequential outcomes. For low-certainty cases, integrate confidence scores directly into the agent’s outputs: many foundation models (e.g., GPT-5) can output a self-assessed certainty score (0– 1) alongside responses by including instructions like “End your response with: certainty: [0–1 score based on confidence in accuracy].” Thresholds can be set (e.g., escalate if certainty < 0.7), or entropy measures used on probabilistic outputs (e.g., high entropy in classification logits indicates ambiguity). Variance across multiple runs (e.g., ensemble 3–5 inferences and escalate if outputs diverge > 20%) or external evaluators (e.g., a secondary foundation model critic scoring coherence) can further quantify uncertainty. In the SOC agent, low-certainty triages (e.g., a threat classification with score < 0.8) could auto-escalate for review, filtering out routine highconfidence cases.

For high-consequence cases, assess impact based on domain-specific severity: in the SOC agent, flag incidents with “high” severity ratings (e.g., potential data breaches) or those affecting critical assets (e.g., admin accounts). Combine this with risk scoring— e.g., multiply uncertainty by consequence (escalate if score > threshold)—to

prioritize. Tools like DSPy can optimize these thresholds offline using historical data, simulating escalation rates to balance load (e.g., aim for < 10% of cases escalated to avoid human fatigue). This hybrid approach ensures AI handles the bulk of routine decisions while humans intervene where judgment is most needed, fostering scalable, trustworthy systems. By defining clear escalation triggers, teams prevent automated systems from making inappropriate or myopic interventions and ensure that nuanced cases receive the attention they deserve.

When a case is escalated, a multidisciplinary review team—often including engineers, product managers, data scientists, and UX experts—systematically analyzes the flagged issue. The review process typically involves the following:

###### _Contextual analysis_

Reproducing the failure or anomaly in a controlled environment to understand the sequence of events and decision points.

###### _Trace inspection_

Examining logs, traces, and decision chains to clarify how the agent interpreted user intent and selected actions.

###### _Impact assessment_

Evaluating the scope and severity of the issue, considering both technical correctness and UX.

###### _Resolution design_

Recommending targeted interventions—ranging from prompt refinement to workflow redesign, new skill development, or even changes to user-facing features. In the SOC example, if drift causes over-isolation of hosts, humans might fix it by updating the isolate_host tool to include a confirmation step.

Effective HITL review protocols emphasize documentation and reproducibility. Decisions are logged, rationales are captured, and outcomes are tracked to ensure that future incidents can be resolved more efficiently and that systemic issues are identified over time.

HITL review often benefits from diverse perspectives beyond pure engineering. Product managers can clarify whether the observed failure reflects a deeper misalignment with user needs. Data scientists may recognize patterns or edge cases invisible to others. UX researchers can surface friction points in user interactions that automated metrics might miss. This collaborative approach ensures that improvements are not just technically correct but are also meaningful and valuable for end users.

The ultimate value of HITL review lies in its contribution to organizational learning. Each reviewed case becomes a data point in an evolving knowledge base—a reference for training new team members, informing system design, and refining feedback loops. Lessons learned are fed back into prompt and tool refinement, skill

development, and system documentation, reducing the recurrence of similar failures in the future.

By balancing automation with human oversight, HITL review ensures that multiagent systems remain both scalable and trustworthy. It transforms feedback pipelines from mere error correction mechanisms into engines of insight, resilience, and continuous improvement.

###### **Prompt and Tool Refinement**

Once feedback pipelines and HITL reviews have surfaced actionable insights, the next step is to implement targeted improvements. In agentic systems, the most direct and impactful levers for system refinement are the design of prompts (the instructions and context provided to language models) and the construction and invocation of external tools (functions, APIs, and actions the agent can use), so refining the prompt can be a very efficient way to improve the overall performance.

###### **Prompt refinement**

Prompts are the bridge between user intent and agent action. Subtle changes in prompt wording, structure, or context can dramatically affect an agent’s interpretation, reasoning, and outputs. Feedback loops commonly reveal issues such as:

- Ambiguous instructions leading to inconsistent or irrelevant responses

- Overly broad prompts causing hallucination or off-task outputs

- Rigid, narrow prompts failing to generalize to real-world variability

- Lack of clarity around task boundaries, escalation, or error handling

Refinement begins with analysis: reviewing misfires, tracing agent reasoning, and isolating which part of the prompt contributed to undesired outcomes. Improvements might include:

###### _Rewriting for clarity_

Making instructions more explicit, reducing ambiguity, and specifying expected response formats

###### _Adding exemplars_

Providing positive and negative examples in the prompt to anchor agent reasoning

###### _Decomposing tasks_

Splitting complex multistep instructions into smaller, sequential prompts or intermediate reasoning stages

###### _Context expansion_

Incorporating additional context, constraints, or relevant background to guide the agent more effectively

DSPy excels at automating prompt refinement by compiling optimized prompts from a set of examples. For the SOC agent, we can use DSPy to refine the internal prompts of a ReAct module, improving how the agent handles alerts by better aligning reasoning and tool calls with expected responses. This is particularly useful for addressing issues like suboptimal tool selection or inconsistent outputs identified in feedback. Here’s an example DSPy code snippet that optimizes a ReAct module for SOC incident handling using a small set of synthetic test cases (expand to 100+ annotated examples in practice for better results):

This code optimizes the ReAct module’s prompts (e.g., for reasoning steps and tool invocation) to better match the provided examples, effectively refining the agent’s behavior without manual prompt tweaking. The resulting optimized_react can be integrated into the SOC agent’s workflow, leading to more reliable handling of diverse alerts and reducing issues like hallucinations or off-task outputs.

In advanced feedback systems, prompt adjustments can even be automated in response to observed failure patterns, though all changes should be validated—preferably in both offline testing and live shadow deployments—to prevent regressions or unintended side effects.

###### **Tool Refinement**

In modern agentic architectures, prompts alone rarely suffice. Agents increasingly rely on a suite of external tools—APIs, code functions, database queries, or custom skills—to retrieve information, perform transactions, or take concrete actions. Feedback pipelines frequently surface issues such as:

- Incorrect or suboptimal tool selection for a given user task

- Parameter mismatches or malformed inputs to tool calls

- Gaps in the toolset—tasks the agent cannot accomplish due to missing or incomplete tools

- Tool chaining failures, where the output of one step is not properly formatted for the next

Tool refinement is a multilevel process:

###### _Refining internal logic_

Optimizing prompts or models within tools to better process and classify data

###### _Expanding capabilities_

Enhancing tools to cover broader scenarios by incorporating optimized reasoning

###### _Integration improvements_

Ensuring tools output reliable, actionable results for the agent’s needs

DSPy supports tool refinement by optimizing how tools are selected and chained within agent modules. Extending the previous example, suppose feedback reveals a gap in the toolset for incident triage (e.g., the agent often skips classification steps, leading to suboptimal decisions). We can add a new mock tool for triage, update the ReAct module to include it, expand the trainset with examples emphasizing proper tool chaining, and reoptimize. This improves tool selection heuristics and integration, making the agent more robust to real-world variability. Here’s the extended DSPy code:

This refinement enhances the tool’s ability to accurately classify threat levels from real API data, handling a wider range of responses—including no-results cases, partial matches, or emerging threats—by optimizing the foundation model’s interpretation prompt.

Each prompt or tool refinement should be documented with a clear rationale—what problem was observed, what change was made, and how its effectiveness will be measured. This discipline ensures improvements are traceable and repeatable, and provides future teams with a knowledge base of what works and why.

Refinements should be validated iteratively, using both offline evaluation (with heldout logs or synthetic cases) and controlled live experiments (e.g., shadow deployments, A/B tests). Monitoring post-deployment performance is critical: even seemingly minor prompt tweaks can have system-wide effects, especially in complex or highly agentic environments.

Over time, the accumulated effect of systematic prompting and tool refinement is substantial. Agents become more reliable, less brittle, and better aligned with user needs. Feedback-driven refinement also reveals higher-level patterns—common sources of misunderstanding or recurring gaps in capability—that can inform architectural improvements and future agent design.

Prompt and tool refinement are the hands-on instruments of progress in agentic systems. By connecting insight to action, and iterating thoughtfully, teams can ensure that every failure or friction point becomes an opportunity for more robust, responsive, and capable AI.

###### **Aggregating and Prioritizing Improvements**

As agentic systems grow in complexity and scale, so does the stream of actionable insights generated by feedback pipelines and human review. Teams quickly discover that not every bug, misfire, or enhancement can—or should—be addressed immediately. Without a system for aggregating and prioritizing improvements, teams risk being overwhelmed by noise, chasing low-impact fixes, or missing systemic problems in favor of surface-level symptoms.

The first step is aggregation: consolidating insights from multiple sources into a unified, accessible view. Feedback may originate from automated monitoring systems, RCA reports, user complaints, HITL reviews, or direct engineer observation. Aggregation platforms (such as centralized dashboards, observability tools, or structured issue trackers) help transform scattered data into a coherent improvement backlog. Key practices include:

###### _Deduplication_

Clustering similar issues together (e.g., recurring prompt failures or repeated tool invocation errors) to avoid fragmented effort

###### _Tagging and categorization_

Labeling issues by root cause, affected workflows, user impact, or system component for easier sorting and filtering

###### _Linking to context_

Attaching supporting logs, traces, user reports, and RCA documentation to each improvement for efficient triage and action

With a unified backlog in hand, the next challenge is prioritization. Not all improvements are created equal—some have outsized impact on system reliability, user satisfaction, or business outcomes. Effective prioritization requires balancing several dimensions:

###### _Frequency_

How often does this issue occur? Frequent but minor issues can add up to significant user friction or operational overhead.

###### _Severity/Impact_

What is the business or user impact? Issues causing critical failures, security risks, or major dissatisfaction should rise to the top.

###### _Feasibility_

How difficult is the fix? Quick wins (low effort, high impact) are often prioritized, while complex improvements may require careful scoping or sequencing.

###### _Strategic alignment_

Does the improvement align with current product goals, upcoming features, or compliance requirements? Sometimes, a fix is essential not for its frequency but for its role in enabling a major initiative or regulatory milestone.

###### _Recurrence and risk_

Are similar failures likely to recur if not addressed? Systemic issues—those rooted in architecture, training data, or agent reasoning—should be flagged for deeper attention.

Prioritization frameworks—ranging from simple impact/effort matrices to more formal Agile or Kanban systems—can help teams reach consensus and adjust plans as system dynamics evolve. It’s essential to treat the improvement backlog as a living artifact, not a static to-do list. Regular review cycles, “bug triage” meetings, and crossteam syncs ensure that priorities are continuously reevaluated in light of new incidents, shifting user needs, or strategic pivots. As improvements are implemented and validated, lessons learned should be fed back into the aggregation process—closing the loop and ensuring that recurring patterns inform future prevention.

The discipline of aggregation and prioritization turns the raw firehose of feedback into a clear, actionable roadmap. By focusing limited resources on the most impactful, feasible, and strategically aligned changes, teams can accelerate system evolution, build user trust, and prevent the accumulation of “technical debt” that can otherwise slow progress. In agentic systems, where the pace of change is rapid and the stakes are high, this process is not a luxury—it’s a necessity.

###### **Experimentation**

Experimentation is the engine of safe progress in multiagent systems. It serves as the bridge between insight and deployment, enabling teams to validate changes, measure their real-world effects, and mitigate risk before rolling out updates broadly. Given the complexity and interconnectedness of agentic architectures, even minor adjustments—such as tweaking a prompt, updating tool parameters, or refining orchestration logic—can produce far-reaching and sometimes unpredictable consequences. Without rigorous experimentation frameworks, teams risk introducing regressions, undermining reliability, or drifting away from user and business objectives.

A well-designed experimentation process provides a structured, incremental pathway for change. Rather than leaping straight from idea to production, changes are introduced and evaluated in controlled environments that closely mimic real-world conditions. This often begins with staging or release candidate (RC) environments— standard best practices where updates are tested in isolated, production-like setups to catch issues early without impacting live users. From there, teams can layer on advanced deployment techniques such as shadow deployments, canary rollouts

(gradual exposure to a subset of traffic), rolling updates (incremental instance-byinstance upgrades), or blue/green deployments (switching between two identical environments). This approach not only uncovers unintended side effects early but also enables direct comparisons between alternative configurations, paving the way for data-driven decision making.

###### **Shadow Deployments**

Imagine rehearsing a play backstage while the live show runs uninterrupted—that’s shadow deployments in action. Here, your updated agent (e.g., with refined reasoning for query ambiguity) shadows the production version, processing identical inputs in parallel. But only the live system’s outputs reach users; those of the shadow are logged for scrutiny, shielding everyone from mishaps.

Shadow deployments are a powerful approach for validating system changes under real-world conditions—without exposing users to risk. This side-by-side comparison enables teams to observe, measure, and diagnose the behavior of new or updated agent logic under authentic operational loads. Shadow deployments are especially valuable for high-impact or high-risk changes—such as updates to planning workflows, integrations with external systems, or significant prompt modifications— where failures could have serious consequences if released unchecked. Key benefits include:

###### _Realistic validation_

Shadow systems experience the full spectrum of real user behavior, surfacing discrepancies and emergent issues that often elude controlled test environments.

###### _Safe exploration_

Engineers can experiment with bold improvements or architectural changes, confident that any errors, regressions, or performance degradations will not reach production.

###### _Edge-case discovery_

Rare or unpredictable scenarios—such as malformed user inputs, ambiguous instructions, or integration quirks—can be detected and analyzed before deployment.

###### _Integration with complementary strategies_

Shadow deployments can be aided by blue-green deployments (maintaining two identical environments and switching traffic only after validation) to enable seamless, zero-downtime rollouts after shadow testing, or canary deployments (gradually routing a small percentage of live traffic to the new version) to support incremental real-time validation in production, reducing overall risk and facilitating smoother transitions from testing to full deployment.

Quality instrumentation is key: compare traces, metrics (accuracy, latency), and outputs rigorously. Triangulate discrepancies to separate breakthroughs from bugs.

Challenges arise in HITL-dependent agents (e.g., those querying users for approvals) —shadows can’t interact without exposure risks. Simulate responses via historical replays or synthetics, or hybridize with staging or A/B testing for interactive flows.

In essence, shadows build confidence quietly, validating in the wild minus the stakes.

###### **A/B Testing**

If shadows are about observing from the sidelines, A/B testing thrusts variants into the spotlight—splitting live traffic between control (A) and treatment (B) versions for head-to-head showdowns. Users interact with one or the other, yielding quantifiable wins on metrics like task success in a collaborative agent swarm or reduced hallucinations in responses. This shines for measurable tweaks, such as running an A/B on prompt variants to optimize user satisfaction in real-time chats, where shadows might miss subtle engagement shifts. a common setup for A/B testing involves randomly assigning users to different agent variants to enable direct, real-world comparisons.

This balanced allocation ensures fair exposure and reliable metrics, enabling teams to confidently identify which variant performs better in practical scenarios. Strengths of A/B testing include:

###### _Real-world relevance_

Results reflect genuine user behavior and input diversity, providing strong evidence of whether changes generalize beyond isolated test cases.

###### _Direct comparison_

Teams can quickly determine which version delivers superior outcomes, under actual operational conditions.

###### _Statistical rigor_

Properly designed A/B tests ensure that observed differences are meaningful— not the result of random variation or biased sampling.

To maximize the value of A/B testing, teams should:

- Define clear, actionable metrics that align with the objectives of the proposed change.

- Ensure sufficient sample size to achieve statistical significance, minimizing the risk of false positives or negatives.

- Prevent cross-contamination (e.g., users switching between versions in a single session) to preserve result integrity.

- Monitor both short- and long-term effects, as some changes may yield quick gains but introduce longer-term issues.

Qualitative review remains important: a decrease in completion rate for version B, for example, may reflect deeper, more thoughtful engagement—rather than outright failure.

However, A/B testing can be more difficult when agents store long-term interaction states, such as chat histories or persistent user contexts, as users might experience inconsistencies if they are reassigned to different versions across sessions. To mitigate this, teams can implement “sticky” user assignments (ensuring users remain in the same variant over time), conduct tests at the session level rather than the user level, or isolate state management to prevent cross-version contamination—potentially by duplicating or versioning state stores for each test group.

Modern experimentation platforms (e.g., LaunchDarkly, Optimizely, or custom dashboards) automate much of the traffic allocation, metric collection, and analysis, freeing teams to focus on interpreting results and acting on insights.

###### **Bayesian Bandits**

What if your A/B test could learn on the fly, shifting users toward winning variants mid-experiment instead of rigidly splitting traffic? That’s the power of adaptive experimentation, where Bayesian Bandits stand out as a smart upgrade for multiagent

systems—dynamically balancing exploration (trying new ideas) with exploitation (sticking to what works) to accelerate improvements in unpredictable environments.

Picture a casino slot machine with multiple “arms” (levers), each offering unknown odds of payout. In Bayesian Bandits, each arm represents a system variant—like alternative prompts for an agent’s query handling or different orchestration strategies in a multiagent swarm. As interactions unfold, the algorithm observes rewards (e.g., successful task resolutions, lower latency, or higher user ratings) and uses Bayesian updates to refine its beliefs about each arm’s performance. Over time, it funnels more traffic to promising arms while sparingly testing others, ensuring you don’t miss hidden gems.

For a concrete agentic example, suppose you’re optimizing an SOC (Security Operations Center) multiagent system, testing three reasoning chains for resolving ambiguous threat queries. The bandit starts evenly, but as data rolls in, say, one chain improves threat classification accuracy by 15%. It reallocates 70% of queries there, still probing the others for shifts in user behavior. This is especially potent in multiagent setups, where interactions can be computationally expensive or reveal emergent behaviors only under load. In fact, frameworks like Knowledge-Aware Bayesian Bandits (KABB) extend this to coordinate expert agents dynamically, using semantic insights to select subsets for tasks like knowledge-intensive queries. Some of the key advantages of Bayesian Bandits include:

###### _Responsiveness_

The system learns and shifts traffic allocations in near real time, reducing opportunity costs and accelerating improvements.

###### _Efficiency_

Rather than “wasting” equal traffic on suboptimal variants, the majority of users experience the best-performing configuration as soon as it is identified.

###### _Scalability_

Well-designed Bayesian Bandit systems can scale to very large numbers of parameters, enabling a much more rapid exploration of the action space than configurating and reviewing a series of fixed experiments.

However, adaptive experimentation also requires:

###### _Metric mastery_

Rewards must reflect true system goals (e.g., user satisfaction, task success) to avoid optimizing for misleading proxies.

###### _Thoughtful initialization_

Neutral priors and regularization help avoid biasing the system prematurely toward any variant.

###### _Vigilant oversight_

Teams must watch for pathological feedback loops or exploitation of short-term trends at the expense of long-term objectives.

Bayesian Bandits shine in fluid, data-rich agentic worlds—think real-time personalization in recommendation agents or adaptive workflows in autonomous teams— delivering faster, smarter evolution than traditional methods.

###### **Continuous Learning**

We now move to continuous learning, where the agentic system is designed to adapt, improve, and optimize performance over time based on real-world interactions, feedback, and evolving user needs. Unlike static models or prescripted workflows, continuously learning agents are designed to ingest new data, refine their behavior, and update reasoning strategies dynamically. This process blends automated adaptation with carefully managed oversight to prevent unintended consequences, such as overfitting to short-term trends or introducing regressions.

Continuous learning encompasses two core mechanisms: in-context learning and online learning. These enable improvements at varying scales—from real-time tweaks within a session to incremental updates across workflows. As discussed in Chapter 7, these build on foundational nonparametric techniques (e.g., exemplar retrieval, Reflexion) and can incorporate parametric methods like fine-tuning where appropriate. Here, we emphasize integrating them into improvement loops, using live production data (e.g., user interactions, telemetry, and failure logs) to tighten the cycle: feedback pipelines surface issues, experimentation validates fixes, and continuous learning embeds them for immediate or ongoing impact.

###### **In-Context Learning**

In-context learning offers the most immediate and flexible means of adaptation in foundation model–based systems. Rather than relying on model fine-tuning or architectural changes, in-context learning empowers agents to modify their behavior dynamically within a single session. By embedding examples, intermediate reasoning steps, or contextual signals directly into prompts, agents can be “taught” new behaviors on the fly—adapting at runtime rather than depending solely on static, pretrained weights.

Consider an agent assisting users with code debugging. If the agent consistently struggles with a particular type of error, an engineer can revise the prompt to include an illustrative example that demonstrates the correct solution. This change takes effect instantly, scoped only to the current session, enabling the agent to improve its responses without requiring broader system retraining. Additionally, agents can leverage user feedback in real time—such as corrections or clarifications—to further

refine their reasoning and adapt their next steps within the same interaction. Key strengths of in-context learning include:

###### _User-specific adaptation_

Tailoring responses to individual user preferences or recurring issues, providing a personalized experience

###### _Real-time feedback incorporation_

Dynamically adjusting behavior in response to user clarifications or follow-up instructions, enhancing responsiveness

###### _Guided reasoning_

Integrating explicit reasoning steps or intermediate outputs to steer the agent toward more reliable or interpretable conclusions

A critical enabler of effective in-context learning is robust context management. Because foundation models have finite context windows, systems must carefully curate which information to include in prompts, how to structure it, and when to remove or compress outdated details. Techniques such as rolling context windows, semantic compression, and vector-based memory retrieval help ensure that the most relevant information remains accessible throughout an interaction.

However, in-context learning comes with inherent limitations. Changes made within a session are ephemeral—once the session ends, any learned adaptations are lost. To preserve valuable insights for future use, successful in-context strategies should be promoted to more permanent mechanisms, such as prompt engineering, workflow updates, or full model retraining.

In practice, in-context learning often serves as a first line of adaptation—enabling rapid, low-risk testing of improvements in live interactions. It acts as a testing ground for new reasoning strategies or prompt structures before these approaches are codified into broader workflows or incorporated system-wide. This makes in-context learning especially useful for handling session-specific failures, rapidly iterating on small refinements, or addressing highly dynamic and unpredictable user inputs where traditional approaches may fall short.

The strengths of in-context learning lie in its instant adaptability, minimal risk, and ability to deliver session-level personalization and real-time refinement. However, these adaptations are inherently transient; any changes made are limited in scope and do not persist once the session concludes. As such, while in-context learning is ideal for rapid prototyping of refinements and responding to evolving or unpredictable user needs, valuable insights derived from these interactions must eventually be formalized through prompt engineering, workflow updates, or model retraining to achieve lasting improvement.

When thoughtfully integrated into a continuous learning pipeline, in-context learning provides not only a powerful mechanism for immediate improvement but also a vital foundation for scalable, longer-term system optimization.

###### **Offline Retraining**

Offline retraining represents a structured, periodic approach to embedding lasting improvements in agent systems, drawing on accumulated data from feedback pipelines and experiments. Unlike in-context adaptations, which are session-bound, offline retraining involves collecting batches of interaction data—such as user queries, agent outputs, and labeled outcomes—and using them to update prompts and tools or even fine-tune underlying models in a controlled, nonproduction environment. This method is particularly suited for addressing systemic issues identified over time, such as recurring misalignments in reasoning or tool usage, without disrupting live operations.

In the SOC agent example, suppose feedback reveals a pattern of false positives in threat triages due to evolving attack vectors. Teams can aggregate historical logs and annotations into a dataset, then use frameworks like DSPy to optimize prompts or fine-tune a lightweight adapter on the base foundation model (as discussed in Chapter 7). The process typically follows these steps:

###### _Data curation_

Gather and label examples from production traces, ensuring diversity and balance to avoid bias.

###### _Model updates_

Apply techniques like few-shot optimization or full fine-tuning on held-out data, focusing on metrics like accuracy or latency.

###### _Validation_

Test the retrained components offline against benchmarks, then via shadow deployments before rollout.

Key strengths include:

###### _Durability_

Changes persist across sessions and users, providing long-term alignment with shifting environments.

###### _Scalability_

Batched updates are efficient for high-volume systems, enabling teams to incorporate large datasets without real-time overhead.

###### _Risk mitigation_

Offline nature enables thorough testing, reducing the chance of regressions.

However, offline retraining requires careful management to prevent overfitting to historical data or ignoring emerging trends. Limitations include computational costs (though mitigated by efficient methods like LoRA) and the need for periodic scheduling to keep models fresh. It’s best used for foundational refinements, such as updating the SOC agent’s prompt with new threat examples or retraining tool classifiers on recent logs.

When integrated with feedback and experimentation, offline retraining closes the improvement loop by translating insights into enduring enhancements. For teams relying on pretrained models, it offers a bridge to customization without constant online adjustments, ensuring agents evolve robustly over time.

###### **Conclusion**

Continuous improvement is not merely a feature of multiagent systems—it is a fundamental requirement for their long-term success. As these systems grow more complex, interact with diverse users, and operate across ever-changing environments, their ability to adapt, learn, and refine themselves becomes essential for maintaining reliability, performance, and alignment with user needs. This chapter has explored the key pillars of continuous improvement: feedback pipelines, experimentation, and continuous learning, each playing a distinct yet interconnected role in driving iterative progress.

Feedback pipelines serve as the diagnostic engine of the improvement cycle, capturing data from live interactions, identifying recurring failure patterns, and surfacing actionable insights through both automated and human-driven processes. From root cause analysis to aggregating and prioritizing improvements, these pipelines create a systematic foundation for identifying _what_ needs to change and _why_ .

Experimentation frameworks provide the controlled environments necessary to validate improvements before full deployment. Techniques like shadow deployments, A/B testing, and Bayesian Bandits enable teams to minimize risk, measure impact, and ensure that every change contributes positively to the overall system.

Finally, continuous learning ensures that improvements extend beyond isolated patches, embedding adaptability directly into the system’s behavior, focusing on incontext learning, which provides instant, session-level refinements.

Crucially, none of these components operate in isolation. Feedback loops feed into experimentation workflows, which in turn guide fine-tuning retraining. Automated pipelines accelerate insight generation, while human oversight ensures that changes are aligned with strategic goals. Documentation serves as the connective tissue across these processes, preserving organizational memory and enabling cross-team collaboration.

Continuous improvement is not a linear process—it’s an ongoing cycle of observation, adjustment, validation, and deployment. As multiagent systems become more deeply integrated into critical workflows, the importance of robust feedback mechanisms, well-designed experiments, and adaptive learning processes will only grow. Organizations that invest in these capabilities will not only reduce failures and improve reliability—they will also unlock the ability to anticipate user needs, respond to emerging trends, and deliver meaningful innovation at scale.

In the end, continuous improvement is as much about systems design as it is about organizational culture. It requires a mindset that views every failure not as a setback but as a signal—an opportunity to learn, iterate, and evolve. By building systems that can observe themselves, learn from their behavior, and adapt with intention, teams can create agent ecosystems that don’t just function—they thrive.

### **CHAPTER 12 Protecting Agentic Systems**

The adoption of AI agents introduces unique security challenges distinct from traditional software. Agentic systems—characterized by their autonomy, advanced reasoning capabilities, dynamic interactions, and complex workflows—significantly expand the threat landscape. Effectively securing these systems requires addressing not only traditional security concerns but also unique vulnerabilities inherent to agent autonomy, probabilistic decision making, and extensive reliance on foundational AI models and data.

Generative AI has introduced a formidable and expanding threat vector in the cybersecurity landscape. These technologies amplify risks through sophisticated attacks like deepfakes for fraud, prompt injections to hijack systems, and memory poisoning in multiagent workflows, where tainted data can cascade into systemic failures or unauthorized actions. For instance, in early 2025, a Maine municipality fell victim to an AI-powered phishing scam that exploited generative voice cloning to steal between $10,000 and $100,000, while the Chevrolet dealership’s chatbot was manipulated via prompt injection to offer a $76,000 vehicle for just $1, highlighting how easily safeguards can be bypassed. Similarly, agentic systems have exposed new vulnerabilities, as seen in Google’s Big Sleep agent uncovering a zero-day flaw in SQLite (CVE-2025-6965), but also raising concerns over autonomous agents potentially escalating privileges or drifting from objectives in enterprise. With Gartner predicting that over 40% of AI-related data breaches by 2027 will stem from cross-border generative AI misuse, and 73% of enterprises already reporting AI security incidents averaging $4.8 million each, addressing these threats is imperative through robust governance, real-time monitoring, and layered defenses to harness AI’s potential without compromising security.

This chapter serves as a comprehensive guide for understanding and mitigating the risks associated with agentic systems. It begins by exploring the unique security

challenges posed by autonomous agents, including goal misalignment, human oversight limitations, and emerging threat vectors targeting AI models. The chapter then delves into strategies to secure foundation models through careful model selection, proactive defensive measures, and rigorous red teaming.

By the end of this chapter, readers will have a robust understanding of the security landscape specific to agent systems and practical strategies to safeguard these powerful but vulnerable technologies.

###### **The Unique Risks of Agentic Systems**

Agentic systems represent a significant leap forward from traditional software by offering autonomous decision making, adaptability, and operational flexibility. These strengths, however, introduce distinct risks:

###### _Goal misalignment_

Agents may interpret their objectives differently than intended, especially when tasked with vague or ambiguous instructions. For example, an agent optimizing user engagement might inadvertently prioritize sensational content, undermining user trust or well-being.

###### _Probabilistic reasoning_

Unlike deterministic systems, agents rely on large-scale foundation models whose outputs are inherently probabilistic. This can result in unintended behaviors such as “hallucinations,” where the agent generates plausible-sounding yet incorrect or misleading information.

###### _Dynamic adaptation_

Autonomous agents continuously adapt to changing environments, complicating the task of predicting and controlling their behavior. Even minor variations in input data or context can significantly alter their decisions and actions.

###### _Limited visibility_

Agents often operate with incomplete information or ambiguous data, creating uncertainty that can lead to suboptimal or harmful decisions.

Addressing these inherent risks requires carefully designed controls, continuous monitoring, and proactive oversight to ensure alignment with human intent. Human oversight is commonly employed as a safeguard against the unintended consequences of agent autonomy. However, HITL systems introduce their own set of vulnerabilities:

###### _Automation bias_

Humans may over-trust agent recommendations, failing to adequately scrutinize outputs, especially if presented with high confidence.

###### _Alert fatigue_

Continuous or low-priority alerts can lead human operators to overlook critical warnings, reducing their effectiveness in preventing errors.

###### _Skill decay_

As agents handle more routine tasks, human skills required for effective oversight may deteriorate, making it challenging to intervene effectively in critical situations.

###### _Misaligned incentives_

Differences between human and agent goals, such as efficiency versus safety, can create conflicts that complicate real-time oversight and decision making.

To mitigate these vulnerabilities, systems should include clear escalation paths, adaptive alerting mechanisms, and ongoing training for human operators to maintain proficiency and readiness. As part of this ongoing training, interactive platforms can provide hands-on experience in recognizing and countering AI vulnerabilities, such as jailbreaking and prompt injections, which directly tie to risks like goal misalignment and probabilistic reasoning. These tools simulate adversarial scenarios to build practical skills in red teaming and defense strategies. Examples are given in Table 12-1.

_Table 12-1. Red team tools_

###### **Emerging Threat Vectors**

As agent systems gain complexity and become integral to critical infrastructures, they attract sophisticated threats specifically designed to exploit their unique architectures and reliance on foundation models. Adversarial attacks are especially common.

Malicious actors may use adversarial prompts—inputs specifically engineered to manipulate AI model behavior—to circumvent security measures, extract sensitive data, or cause harmful actions, and take many forms, as showcased in Table 12-2:

_Table 12-2. Emerging AI threat vectors_

These examples highlight the evolving sophistication of prompt-based attacks, which can exploit even well-guarded systems by blending seamlessly with legitimate inputs. Understanding and simulating such vulnerabilities through red teaming is crucial for developing resilient defenses in agentic architectures. New types of attacks continue to be discovered as the field advances, creating a perpetual cat-and-mouse game between model trainers—who refine safeguards and alignments—and attackers who innovate novel exploits. To stay ahead, organizations must vigilantly monitor emerging threats, conduct regular security audits, and implement timely updates to their systems, including fine-tuning models with the latest adversarial datasets and deploying adaptive defensive layers.

###### **Securing Foundation Models**

The foundation of a secure agent system begins with selecting the appropriate foundation models. Different models come with varying strengths, limitations, and risk profiles, making the selection process a pivotal decision for security. Broadly, model selection involves evaluating trade-offs across capabilities, deployment constraints, transparency, and risk factors.

First, the capabilities of the model must align with the agent’s intended tasks. More powerful, general-purpose models offer versatility but may also present greater risks due to their complexity and potential for unpredictable outputs. In contrast, smaller, fine-tuned models are often more predictable and easier to monitor but may lack the flexibility to handle diverse tasks.

Access control is another critical consideration. Open source models provide greater transparency and allow for independent audits, but they may lack built-in safeguards and require significant security hardening during deployment. Proprietary models, while offering robust built-in protections and support, may operate as black boxes, limiting visibility into their internal decision-making processes.

The deployment environment also influences model selection. For highly sensitive applications, on-premises or air-gapped deployments are often preferable to mitigate the risks associated with external dependencies or cloud-based vulnerabilities. Conversely, cloud-based deployments may offer scalability and ease of maintenance but

require strict access controls and encryption measures to secure data in transit and at rest.

A vital but often overlooked factor is alignment with compliance and regulatory standards. Certain use cases may require models that meet specific certifications, such as GDPR (General Data Protection Regulation) compliance for data privacy or SOC 2 certification for operational security. Selecting models that inherently align with these standards reduces downstream risk and compliance burdens.

Lastly, model explainability and interpretability play a key role in risk mitigation. Models that provide greater transparency in their reasoning processes make it easier to identify and address vulnerabilities or unintended behaviors.

In practice, the decision rarely boils down to choosing a single model. Many agent systems adopt a hybrid approach, using specialized smaller models for high-stakes tasks requiring precision and leveraging larger general-purpose models for tasks demanding creativity and contextual flexibility.

Effective model selection is not a onetime decision but an ongoing process. As models evolve and new vulnerabilities emerge, continuous evaluation and adaptation of the chosen foundation models are essential for maintaining robust security. Organizations must remain vigilant, ensuring their models align with both operational goals and the dynamic landscape of security threats.

###### **Defensive Techniques**

Securing foundation models requires a multilayered approach that blends technical safeguards, operational best practices, and continuous monitoring. Defensive techniques aim to prevent malicious exploitation, reduce unintended behaviors, and ensure that models operate reliably across diverse contexts. These techniques span from preprocessing and input validation to runtime monitoring and output filtering, creating a robust security posture for foundation model–powered agent systems.

One of the foundational defensive strategies is input sanitization and validation. Agents are often vulnerable to adversarial inputs—carefully crafted prompts designed to manipulate model behavior. By implementing robust input validation layers, systems can detect and neutralize harmful prompts before they reach the model. This can include filtering for common attack patterns, enforcing strict syntax rules, and rejecting inputs containing malicious instructions.

Another critical defense is prompt injection prevention. Prompt injection occurs when an attacker embeds malicious instructions within an otherwise normal-looking input, tricking the model into overriding its intended directives. To counteract this, developers can use techniques such as instruction anchoring—where the model’s primary instructions are strongly reinforced throughout the prompt—or prompt templates that strictly control how inputs are formatted and interpreted. Here’s one

example of how this can be implemented with LLM Guard, an open source library in Python:

This implementation showcases a straightforward yet effective way to bolster prompt security. By combining anonymization for personally identifiable information (PII) protection and substring banning for injection patterns, developers can significantly reduce vulnerability exposure. For production environments, consider expanding the scanners with additional LLM Guard modules (e.g., toxicity detection or jailbreak prevention), tuning thresholds based on empirical testing, and integrating this into a multilayered defense strategy. Regular updates to the library and red teaming will ensure ongoing resilience against evolving threats, ultimately fostering safer deployment of foundation model–powered agents.

To evaluate the efficacy of these defenses, prompt injection test benchmarks, such as the Lakera PINT Benchmark, can be employed. This open source tool uses a diverse dataset of 4,314 inputs—including multilingual prompt injections, jailbreaks, and hard negatives—to compute a PINT Score measuring detection accuracy, with results showing varying performance across systems like Lakera Guard (92.5%) and Llama Prompt Guard (61.4%). As the field is still in its early days, it’s challenging to determine how well-guarded a system truly is, emphasizing the need for ongoing testing and updates. Similarly, BIPIA (Benchmark for Indirect Prompt Injection Attacks) from Microsoft is one of the most referenced, focusing specifically on evaluating foundation model robustness against indirect injections with a dataset of attacks and defenses.

Output filtering and validation are equally essential. Even with careful input controls, models may still generate harmful or unintended outputs. Output filtering techniques, including automated keyword scanning, toxicity detection models, and rulebased filters, can help catch problematic content before it reaches the end user. Additionally, implementing postprocessing pipelines ensures outputs are validated against business rules and safety constraints.

Access control and rate limiting are also important operational defenses. By tightly regulating access to foundation model endpoints—through authentication mechanisms, role-based permissions, and API rate limits—systems can reduce the risk of abuse and prevent brute-force attacks. Logging and auditing every interaction with the model further enables security teams to detect suspicious patterns and respond proactively.

Sandboxing foundation model operations isolates agent activities in controlled environments, preventing unintended actions from spilling into broader systems. This is particularly useful when agents interact with external plug-ins or APIs, ensuring that a misbehaving agent cannot cause cascading failures across dependent services.

In practice, effective defensive strategies are rarely static—they require continuous iteration and adaptation. As threat actors evolve their tactics, defensive systems must remain agile, incorporating insights from real-world adversarial testing, security audits, and emerging best practices. By adopting a layered defense strategy that integrates technical, operational, and human-centric safeguards, organizations can significantly reduce the risks associated with deploying foundation models in agent systems.

###### **Red Teaming**

Red teaming is a proactive security practice where experts simulate adversarial attacks to identify vulnerabilities, weaknesses, and failure modes in agent systems and their underlying foundation models. Unlike traditional software testing, which focuses on functional correctness, red teaming focuses on probing the system’s robustness

against intentional misuse, adversarial manipulation, and edge-case scenarios. This approach is especially critical for foundation models, given their probabilistic nature and susceptibility to subtle prompt manipulations.

At its core, red teaming involves designing and executing adversarial scenarios that mimic real-world attack strategies. These scenarios can include techniques such as prompt injection, where attackers craft deceptive inputs to manipulate model behavior, or jailbreaking, where attempts are made to bypass the model’s safety filters and elicit restricted outputs. Red team exercises also assess the model’s behavior under stress conditions, such as ambiguous instructions, contradictory prompts, highstakes decision-making context, or proclivity to leak sensitive data or violate operational constraints.

This cyclical process ensures vulnerabilities are systematically addressed, adapting to evolving threats in foundation models and agent behaviors. Red teaming frequently incorporates the use of language models to create synthetic datasets that intentionally do not conform to what developers expect to encounter. These datasets—designed to include anomalous patterns, noisy inputs, biased distributions, or out-of-domain examples—serve as a powerful stress test for the system’s robustness across a wide range of scenarios. For instance, a foundation model could generate malformed queries mimicking real-world user errors particular to your use case or adversarial manipulations, revealing how the agent handles inputs that deviate from training assumptions. This approach ensures comprehensive coverage of edge cases, going beyond individual prompts to simulate broader data environments, and can be automated for scalability in ongoing evaluations.

To ensure comprehensive coverage, automated red teaming tools are increasingly used alongside human testers. These tools can systematically generate adversarial prompts, test thousands of input variations, and evaluate the model’s responses at scale. However, human creativity remains irreplaceable in identifying nuanced vulnerabilities that automated tools might overlook. Several specialized frameworks

enhance red teaming for foundation models and agentic systems, automating attacks and evaluations to uncover risks like jailbreaks, hallucinations, and hijacking. The following are some of the leading open source frameworks to facilitate and accelerate red teaming and hardening:

###### _DeepTeam_

This is a lightweight, extensible foundation model red-teaming framework for penetration testing and safeguarding foundation model systems. DeepTeam automates adversarial attacks such as jailbreaks, prompt injections, and privacy leaks, then helps you build guardrails to prevent them in production. It integrates seamlessly with existing workflows, allowing custom scripts for multiturn agent testing—e.g., simulating context manipulation to elicit prohibited outputs. Its repo is located at _https://oreil.ly/O8nlL_ .

###### _Garak_

NVIDIA’s “Generative AI Red-Teaming and Assessment Kit” probes foundation models for hallucinations, data leakage, prompt injections, misinformation, toxicity, jailbreaks, and more—analogous to Nmap/MSF (Network Mapper/Metasploit Framework) for foundation models. With its modular design, it’s ideal for scaling tests across foundation models, such as evaluating probabilistic reasoning under stress conditions. The source code can be found at _https://oreil.ly/rGIY4_ .

###### _PyRIT_

This is Microsoft’s Prompt Risk Identification Tool, an open source framework for automating red team attacks on generative AI systems, including foundation models. It supports orchestrators for generating prompts, scorers for evaluating responses, and targets for endpoints like Azure ML or Hugging Face. While focused on security testing, it’s flexible for scripting custom evals covering safety, bias, hallucinations, tool use, and beyond. For red teaming, use it to assess jailbreaking resistance or sensitive information disclosure in dynamic adaptation scenarios, with built-in support for multimodal and agentic exploits. The repo can be found at _https://oreil.ly/oHpdu_ .

Effective red teaming doesn’t stop at identifying vulnerabilities—it also includes documentation, reporting, and mitigation planning. Findings from red team exercises should feed into iterative improvements, informing updates to model configurations, input/output filters, and training datasets. Teams must also prioritize vulnerabilities based on their severity, exploitability, and potential real-world impact.

Beyond technical vulnerabilities, red teaming can also uncover social engineering risks. For example, an attacker might manipulate a foundation model–powered agent into revealing sensitive information through cleverly worded prompts or mimic trusted communication styles to deceive human operators.

Finally, red teaming is not a onetime exercise—it must be an ongoing process. As models are fine-tuned, updated, or deployed in new contexts, their security profile changes, necessitating regular red team reviews. Continuous collaboration between red teams, model developers, and operational security experts ensures that vulnerabilities are identified and addressed before they can be exploited in real-world scenarios.

In essence, red teaming acts as both a stress test and an early warning system for foundation model–powered agent systems. It fosters a culture of proactive security, where weaknesses are discovered and mitigated internally before they can be exploited externally. Organizations that integrate robust red teaming practices into their development lifecycle are far better equipped to handle the complex and evolving threats facing modern agent systems.

###### **Threat Modeling with MAESTRO**

As agentic AI systems grow in complexity, traditional threat modeling frameworks like STRIDE or PASTA often fall short in addressing their unique attributes, such as autonomy, dynamic learning, and multiagent interactions. MAESTRO (Multi-Agent Environment, Security, Threat, Risk, and Outcome), a specialized framework released by the Cloud Security Alliance (CSA), was designed explicitly for threat modeling in agentic AI.

MAESTRO provides a layered reference architecture to systematically identify vulnerabilities, assess risks, and implement mitigations across the AI lifecycle. By breaking down agentic systems into seven interconnected layers, it enables developers, security engineers, and AI practitioners to build resilient architectures that anticipate evolving threats, such as those amplified by generative AI’s content creation capabilities or agentic autonomy in enterprise settings.

The framework’s purpose is to foster proactive security by mapping threats, risks, and outcomes in a modular way, ensuring separation of concerns while highlighting interlayer dependencies. This is particularly relevant for agentic systems, where a vulnerability in one layer (e.g., data poisoning in foundational models) can cascade into others (e.g., unauthorized actions in the ecosystem).

Real-world incidents underscore its necessity. For instance, the 2024 Hong Kong deepfake heist, where generative AI was used to impersonate executives and siphon $25 million, illustrates how unmodeled threats in data operations and agent frameworks can lead to catastrophic financial losses. Similarly, enterprise deployments of agentic AI, like those in supply chain management, have exposed risks of “memory poisoning,” where tainted data persists across agents, as seen in simulated attacks during 2025 CSA wargames. Table 12-3 summarizes the key threats, recommended mitigations, and real-world or illustrative examples for each of MAESTRO’s seven layers.

_Table 12-3. MAESTRO Agentic AI Threat Modeling Framework_

Best practices for using MAESTRO include integrating it iteratively into the software development lifecycle and updating models based on emerging threats like those in OWASP’s 2025 LLM Top 10. Start with a high-level system diagram, assess each layer’s assets and entry points, prioritize risks using a scoring system (e.g., Common Vulnerability Scoring System [CVSS] for AI), and simulate attacks via red teaming (as in the previous section). In practice, tools like Microsoft’s Threat Modeling Tool can be adapted for MAESTRO, ensuring agentic systems remain secure amid 2025’s rising AI threats, where 97% of enterprises report incidents averaging $4.4 million. By adopting MAESTRO, organizations can transform reactive defenses into a proactive, layered strategy, directly supporting the safeguards discussed in “Securing Agents” on page 288.

###### **Protecting Data in Agentic Systems**

Data serves as both the fuel and the foundation of agent systems, driving decision making, enabling contextual reasoning, and ensuring meaningful interactions with users. However, the reliance on large datasets, continuous data exchange, and complex multiagent workflows introduces significant risks to data privacy, integrity, and security. Agents often handle sensitive information, including personal data, proprietary business insights, or confidential records, making them attractive targets for malicious actors and prone to accidental data leaks. Protecting data in agentic systems is not merely a technical challenge—it’s a fundamental requirement for building trust, ensuring compliance with regulations, and maintaining operational integrity.

In this section, we will explore key strategies for securing data across the agent lifecycle, beginning with data privacy and encryption, followed by measures for ensuring data provenance and integrity, and concluding with techniques for handling sensitive data securely.

###### **Data Privacy and Encryption**

In agentic systems, data privacy and encryption form the first line of defense against unauthorized access, data breaches, and unintended data exposure. These systems often interact with multiple data sources—structured databases, real-time user inputs, and third-party APIs—each introducing potential vulnerabilities. Ensuring that data

remains confidential, both at rest and in transit, is paramount for maintaining trust and regulatory compliance.

At rest, data encryption ensures that sensitive information stored in agent systems remains unreadable to unauthorized parties. Encryption standards such as AES-256 (Advanced Encryption Standard) provide robust protection for stored data, whether it resides in a local database, cloud storage, or temporary memory buffers used during agent operations. Additionally, access control mechanisms should be enforced, ensuring that only authorized agents or team members can access encrypted data. This typically involves role-based access control (RBAC) and fine-grained permission settings.

During transit, end-to-end encryption (E2EE) safeguards data as it moves between agents, external APIs, or storage systems. Protocols such as TLS (Transport Layer Security) ensure that data remains secure even when transmitted across public networks. For highly sensitive workflows, additional layers of protection, such as mutual TLS (mTLS) authentication, can further verify the identity of both sender and receiver.

However, encryption alone is insufficient without data minimization practices. Agent systems should be designed to process only the minimum amount of sensitive data required to complete their tasks. Reducing the data footprint not only limits exposure but also simplifies compliance with privacy regulations such as GDPR or CCPA (California Consumer Privacy Act). For instance, anonymization and pseudonymization techniques can obscure personal identifiers without compromising data utility.

Another essential consideration is secure data retention and deletion policies. Agent systems often generate logs, intermediate outputs, and cached data that may contain sensitive information. These artifacts must be encrypted, monitored, and periodically purged according to predefined data retention policies to prevent unintentional data leaks.

Furthermore, organizations must implement data governance frameworks to manage how data flows across different agents and subsystems. This includes auditing data access logs, enforcing encryption standards across all agent workflows, and regularly reviewing compliance with privacy policies. Effective governance ensures that data is not only protected from external threats but also handled responsibly within the organization.

In summary, data privacy and encryption are nonnegotiable pillars of secure agentic systems. By implementing strong encryption standards, minimizing data exposure, enforcing access controls, and adopting emerging technologies, organizations can build robust protections against data-related threats. These measures not only secure sensitive information but also reinforce user trust and ensure alignment with evolving global privacy regulations.

###### **Data Provenance and Integrity**

In agentic systems, data provenance and integrity are essential for ensuring that the information agents rely on is accurate, trustworthy, and free from tampering. As agents increasingly interact with diverse data sources—ranging from user inputs and internal databases to third-party APIs and real-time streams—the ability to trace the origin of data and verify its authenticity becomes a cornerstone of security. Without proper provenance and integrity mechanisms, agents risk making decisions based on corrupted, manipulated, or unverified data, leading to potentially catastrophic outcomes in high-stakes environments such as finance, healthcare, or critical infrastructure.

Data provenance refers to the ability to track the lineage and history of data, including where it originated, how it has been processed, and which transformations it has undergone. Establishing robust data provenance mechanisms enables organizations to answer questions such as: Where did this data come from? Who or what modified it? Is it still in its original, unaltered state?

Provenance metadata often includes timestamps, source identifiers, transformation logs, and cryptographic signatures. This level of transparency helps auditors and developers understand data flows and trace back anomalies or malicious activity.

Complementing provenance is data integrity, which focuses on ensuring that data remains unchanged and untampered throughout its lifecycle. Cryptographic hashing techniques, such as SHA-256 (Secure Hash Algorithm), are widely used to create unique fingerprints for data objects. If even a single bit of the data changes, the hash will no longer match, serving as a clear indicator of tampering. Digital signatures further reinforce integrity by allowing recipients to verify both the origin and the unchanged state of the data.

In practice, immutable storage systems, such as append-only logs, are often employed to strengthen both provenance and integrity. These systems prevent unauthorized modifications to historical records, ensuring that past data states remain verifiable. For example, agents interacting with financial transaction data can reference an immutable ledger to verify that records have not been altered post-entry.

Integrity verification workflows provide structured processes to enforce these mechanisms in agentic systems. For example, a typical data ingestion workflow might involve the following:

1. Computing a SHA-256 hash of incoming data upon receipt

2. Attaching a digital signature using asymmetric cryptography (e.g., RSA [RivestShamir-Adleman] or ECDSA [Elliptic Curve Digital Signature Algorithm]) to confirm origin

3. Storing the hash and signature in a metadata layer

4. Revalidating the hash and signature at each processing stage—flagging mismatches via automated alerts if tampering is detected

In multiagent setups, this can be orchestrated with tools like Apache NiFi, where flows define integrity checks (e.g., via custom processors) before data is passed between agents, ensuring end-to-end verification. Another workflow example in AI pipelines uses libraries like Python’s cryptography module to automate batch verifications, such as during model training where agents cross-check dataset hashes against expected values to prevent poisoned inputs from propagating.

Agents operating in multiparty workflows or consuming third-party data sources face additional challenges in maintaining data integrity. Third-party validation mechanisms can help mitigate these risks by introducing independent checks before data is ingested into an agent system. For instance, agents could use cryptographic attestation to verify the authenticity of data received from external APIs or rely on federated trust systems to cross-verify data across multiple independent sources.

Additionally, real-time integrity checks play a crucial role in preventing agents from acting on corrupted data. These checks involve validating data hashes, verifying timestamps, and ensuring consistency across data replicas before execution proceeds. Automated alerting systems can flag suspicious data patterns, unauthorized changes, or inconsistencies in real time, allowing human operators or other agents to intervene before further damage occurs.

In summary, data provenance and integrity are critical for building reliable, secure, and accountable agent systems. By implementing cryptographic hashing, immutable storage, third-party validation, and real-time integrity checks, organizations can ensure that agents operate on accurate and trustworthy data. These practices not only mitigate the risk of data corruption and tampering but also lay the foundation for building transparent and auditable agent ecosystems.

###### **Handling Sensitive Data**

Agent systems often interact with sensitive data, ranging from PII and financial records to proprietary business intelligence and confidential communications. As these systems become more deeply embedded in workflows across industries such as healthcare, finance, and legal services, the responsible handling of sensitive data is not just a best practice—it is an operational necessity. Mishandling such data can result in severe legal, financial, and reputational consequences, making robust safeguards essential.

At the foundation of secure data handling is the principle of data minimization. Agents should be designed to access, process, and store only the data required to complete their tasks, nothing more. This approach reduces the overall risk exposure

and limits the potential damage of a data breach. Techniques such as pseudonymization and anonymization further support this principle by obscuring sensitive identifiers while retaining the utility of the data for analysis or processing. For example, a healthcare agent might anonymize patient identifiers while still processing treatment history to recommend care options.

Equally important is the implementation of role-based access control (RBAC) and attribute-based access control (ABAC) systems. These controls ensure that only authorized agents, users, or subsystems can access specific categories of sensitive data. For instance, an agent tasked with customer support might only have access to customer interaction history, while another handling billing might require financial details. Additionally, granular permissions—such as read-only or write-only access— can further reduce risk by limiting the scope of potential misuse.

Encryption protocols must be enforced throughout the data lifecycle. Data in transit, whether flowing between agents, APIs, or databases, should always be protected using encryption standards such as TLS. For data at rest, strong encryption algorithms like AES-256 ensure that even if an unauthorized party gains access to storage systems, the data remains unreadable.

Another critical consideration is secure logging and auditing. Sensitive data should never appear in plain text within logs, error messages, or debugging outputs. Organizations must establish clear policies to govern log sanitization, ensuring that debugging tools do not inadvertently expose confidential information. Regular audits of logs, combined with automated anomaly detection systems, can flag suspicious access patterns or potential data leaks in real time.

To maintain immutable audit trails in multiagent systems without relying on decentralized technologies, organizations can leverage cryptographic chaining techniques, such as Merkle trees, where each data entry is hashed and linked to the previous one, creating a tamper-evident structure that agents can traverse to verify historical integrity. Event sourcing systems like Apache Kafka with append-only topics further enable this by storing state changes as immutable sequences of events, enabling agents to reconstruct and audit workflows retrospectively—e.g., replaying transaction histories to detect anomalies. These approaches ensure comprehensive logging across agent interactions, with tools like ELK Stack (Elasticsearch, Logstash, Kibana) for querying and visualizing trails, promoting accountability in complex, distributed environments.

Agents must also handle data retention and deletion policies with precision. Sensitive data should not persist longer than necessary, and automated deletion routines must be implemented to ensure compliance with data protection regulations such as GDPR and CCPA. Temporary data caches or intermediate outputs generated during agent workflows must also be purged once their purpose is served.

In multiagent or multiparty workflows, data-sharing protocols must be tightly controlled. Agents operating across organizational boundaries—or those interacting with third-party plug-ins or APIs—must adhere to strict data-sharing agreements. Secure multiparty computation (SMPC) and federated learning offer innovative approaches to enable agents to process sensitive data collaboratively without directly exposing raw information.

The human element remains a crucial part of data security. Developers and operators managing agent systems must be trained in secure data handling practices and be aware of common pitfalls, such as unintentional data exposure through poorly configured endpoints or verbose error messages. Clear accountability structures must also be in place to define responsibilities and escalation procedures in the event of a data breach or security incident.

Handling sensitive data in agent systems requires a holistic approach that combines technical safeguards, operational policies, and regulatory compliance. By embracing data minimization, encryption, granular access controls, secure logging, and transparent retention policies, organizations can ensure that sensitive information remains protected throughout the agent’s lifecycle. These practices not only mitigate legal and reputational risks but also build user trust—a critical component for the long-term success of agent systems in sensitive domains.

###### **Securing Agents**

While securing the underlying foundation models and protecting data are essential components of agent system security, the agents themselves must also be fortified against vulnerabilities, misuse, and failure. Agents often operate autonomously, interact with external systems, and make decisions in complex environments, introducing unique security challenges. These systems must be designed with robust safeguards, equipped to detect and respond to threats, and resilient enough to recover from unexpected failures. This section begins with safeguards—mechanisms designed to proactively prevent misuse, misconfiguration, or adversarial manipulation of agents.

###### **Safeguards**

Safeguards are preemptive controls and protective measures designed to minimize risks associated with agent autonomy, interactions, and decision-making processes. While agents offer remarkable flexibility and scalability, their ability to operate independently also makes them vulnerable to exploitation, misalignment, and cascading failures if appropriate safeguards are not in place.

One foundational safeguard is role and permission management. Each agent should have clearly defined operational boundaries, specifying what tasks it can perform, what data it can access, and what actions it is authorized to take. This principle is

often implemented using RBAC, where permissions are tightly scoped and reviewed periodically. For example, an agent responsible for customer service should not have access to financial records or system administrative functions.

Another critical safeguard is agent behavior constraints, which define strict operational limits within which an agent must operate. These constraints can be implemented through policy enforcement layers that validate every decision or action against predefined rules. For instance, an agent instructed to summarize text should not attempt to execute code or make external network requests. Constraints can also include response validation filters, ensuring that agents adhere to ethical guidelines, regulatory requirements, and operational policies.

Environment isolation is another effective safeguard, achieved through mechanisms like sandboxing or containerization. By isolating agent operations from the broader system, organizations can prevent unintended consequences from spreading across interconnected workflows. Sandboxed environments limit the agent’s access to sensitive resources, APIs, or external networks, reducing the blast radius of any potential failure or exploitation.

Safeguards also include input/output validation pipelines, which act as gatekeepers for agent interactions. Input validation ensures that malicious prompts, malformed data, or adversarial instructions are sanitized before reaching the agent. Similarly, output validation mechanisms filter the agent’s responses to detect and block unintended actions, harmful content, or policy violations before they propagate downstream.

Rate limiting and anomaly detection serve as dynamic safeguards to prevent agents from being overwhelmed by malicious actors or rogue processes. Rate limiting restricts the number of interactions an agent can process within a given time frame, preventing resource exhaustion or DoS scenarios. Meanwhile, anomaly detection tools monitor agent behavior and flag deviations from expected operational patterns. For instance, an agent suddenly initiating a large number of external API calls might trigger an alert for further investigation.

Furthermore, audit trails and logging mechanisms play an essential role in maintaining accountability and traceability. Every significant decision, input, output, and operational event should be logged securely. These logs must be immutable, encrypted, and regularly reviewed to identify suspicious activity or recurring failure patterns. Transparent logging also supports compliance audits and forensic investigations in the event of a security incident.

Lastly, fallback and fail-safe mechanisms must be in place to ensure graceful degradation in the event of a failure. If an agent encounters an ambiguous scenario, exceeds its operational limits, or detects an anomaly, it should revert to a safe state or escalate

the issue to a human operator. Fallback strategies can include reverting to predefined workflows, triggering alert notifications, or temporarily halting certain operations.

However, safeguards are not static—they must evolve in response to emerging threats, shifting operational requirements, and real-world incidents. Organizations must conduct regular reviews, penetration testing, and red teaming exercises to ensure safeguards remain effective under evolving conditions.

In essence, safeguards are the foundation of secure agent systems, acting as proactive barriers against misuse, misalignment, and exploitation. By implementing robust role management, behavior constraints, sandboxing, anomaly detection, and fallback mechanisms, organizations can create agents that operate securely, predictably, and within well-defined boundaries. These safeguards not only protect agents from external threats but also minimize the risks associated with unintended behaviors and internal misconfigurations, building confidence in the deployment and operation of agentic systems.

###### **Protections from External Threats**

Agent systems are inherently exposed to external threats due to their reliance on APIs, data streams, third-party plug-ins, and dynamic user inputs. These connections, while essential for the agent’s functionality, also create numerous entry points for malicious actors to exploit. External threats can range from adversarial attacks designed to manipulate agent behavior, to data exfiltration attempts, to distributed denial-of-service (DDoS) attacks targeting agent endpoints. Protecting agents from these threats requires a layered defense strategy that combines technical controls, real-time monitoring, and proactive mitigation techniques.

A key aspect of this layered strategy is a secure network architecture that isolates public-facing components from sensitive internal resources. This design minimizes exposure by placing web servers in the DMZ for handling external interactions, while routing internal communications through dedicated controls to protect databases and other critical assets.

To further enhance the protections the internal network can also be divided into subnets for additional isolation and control. This segmentation—such as placing web servers in one subnet and the database in another—limits the blast radius of any potential internal compromise, ensuring that even if an attacker gains access to one area (e.g., a web server), they cannot easily pivot to others without passing through the internal router’s access control lists (ACLs) and monitoring checks. Subnetting complements the overall zero-trust model by enforcing granular network policies, such as restricting traffic to specific ports or protocols, and

integrating with anomaly detection to flag unusual inter-subnet communications. This architecture not only enforces perimeter security but also enables granular controls like ACLs on routers and mTLS for inter-component communication, reducing the risk of lateral movement by attackers who breach the outer layers.

At the forefront of external threat protection is network security. Agents must operate within protected network boundaries, using technologies such as firewalls and intrusion detection and prevention systems (IDPS) to filter malicious traffic and block unauthorized access attempts. Endpoints where agents interact with external APIs or services must enforce mTLS authentication to ensure both sides of the connection are verified. Additionally, rate limiting and throttling controls should be implemented on public-facing interfaces to prevent resource exhaustion caused by excessive API requests or malicious traffic surges.

Authentication and authorization mechanisms are also critical safeguards against external threats. Agents must enforce strict identity verification protocols, such as OAuth 2.0 or API keys, to ensure only authorized users and services can interact with them. RBAC should extend to external systems, limiting what each external entity can access and how they can interact with the agent.

A particularly insidious external threat comes from supply chain attacks, where malicious code or vulnerabilities are introduced through third-party libraries, plug-ins, or dependencies. To mitigate this risk, agent systems should adopt software composition analysis (SCA) tools that continuously scan dependencies for known vulnerabilities and enforce signature verification for third-party integrations. Additionally, organizations should maintain a software bill of materials (SBOM) to track all third-party components and their security statuses.

Adversarial attacks—including prompt injection, data poisoning, and manipulation through ambiguous inputs—require specialized defenses. Input validation pipelines should sanitize all incoming data to prevent malicious prompts from reaching the agent’s reasoning layer. For example, adversarial inputs designed to trick the agent

into leaking sensitive information or executing unintended commands must be detected and filtered before processing. Techniques like instruction anchoring and context isolation can further reduce the risk of prompt injection attacks.

Real-time anomaly detection systems are essential for identifying suspicious behavior originating from external interactions. These systems monitor patterns in incoming traffic, user prompts, and agent responses, flagging anomalies such as repeated failed authentication attempts, unexpected API calls, or patterns that match known attack vectors. Organizations can also use honeytokens—fake pieces of sensitive information embedded in data flows—to detect unauthorized access attempts by observing if they are accessed or exfiltrated.

Beyond technical measures, endpoint hardening ensures that the infrastructure that is supporting agents remains resilient against compromise. This includes enforcing least-privilege principles on the underlying servers, keeping operating systems and dependencies updated with security patches, and disabling unnecessary services or ports that could serve as entry points for attackers.

Proactive security testing and audits play a crucial role in strengthening protections against external threats. Organizations should regularly perform penetration testing, vulnerability scans, and red teaming exercises specifically targeting external access points and data flows. Insights gained from these activities must feed back into improving security measures and closing identified vulnerabilities.

Finally, incident response plans must include procedures for handling external breaches or attempted intrusions. Organizations should have predefined protocols for isolating compromised agents, escalating alerts, and initiating recovery workflows. Clear documentation and drills ensure teams can respond swiftly and effectively under pressure.

In summary, protecting agents from external threats requires a multilayered defense strategy that combines network security, authentication controls, adversarial defenses, anomaly detection, and continuous monitoring. By isolating external interfaces, validating all incoming data, hardening infrastructure, and conducting regular security testing, organizations can significantly reduce their exposure to external attacks. As agent systems continue to grow in scale and complexity, proactive protection against external threats becomes not just a best practice, but an operational imperative.

###### **Protections from Internal Failures**

While external threats often dominate discussions around agent system security, internal failures can be equally damaging, if not more so, due to their potential to bypass external defenses and propagate silently across interconnected workflows. Internal failures stem from a variety of causes, including misconfigurations, poorly

defined objectives, insufficient safeguards, conflicting agent behaviors, and cascading errors across multiagent systems. Protecting agents from internal failures requires a holistic approach that combines robust system design, ongoing validation, and mechanisms for graceful failure and recovery.

One of the primary sources of internal failure arises from misaligned objectives and constraints within the agent’s instructions or operational goals. If an agent’s directives are ambiguous, overly narrow, or misinterpreted during execution, it may pursue unintended behaviors. For example, an optimization-focused agent might prioritize speed over safety, leading to risky or harmful outcomes. To mitigate this, clear operational boundaries and behavioral constraints must be embedded into the agent’s architecture. These constraints should be reinforced through policy enforcement layers that validate agent decisions against predefined rules before execution.

Error handling and exception management are critical safeguards against internal failures. Agents must be equipped to detect and handle unexpected conditions, such as invalid inputs, API failures, or data inconsistencies, without cascading these errors downstream. Well-defined fallback strategies ensure that agents can gracefully degrade their functionality instead of failing catastrophically. For example, if an external API dependency becomes unavailable, the agent could switch to a cached dataset, notify an operator, or delay noncritical operations until the dependency is restored.

Monitoring and telemetry systems serve as early-warning mechanisms for internal failures. Real-time logs, error reports, and performance metrics must be continuously monitored to detect anomalies or performance degradation before they escalate into larger problems. Health checks—periodic automated tests to ensure an agent’s core functions are operating correctly—should be implemented to proactively identify failure points. Additionally, agents should report self-assessment signals, flagging when they encounter ambiguous instructions, incomplete data, or conflicting goals. To make monitoring more effective, organizations should track specific key performance indicators (KPIs) tailored to agentic systems. Common metrics include:

###### _Error rates_

Measure the percentage of failed tasks or hallucinations (e.g., incorrect outputs despite valid inputs), with alerts triggered if rates exceed 5% over a rolling onehour window.

###### _Response latency_

Track average and P99 (99th percentile) response times, alerting if they surpass two seconds for critical operations, indicating potential bottlenecks or overloads.

###### _Resource utilization_

Monitor CPU, GPU, and memory usage, with thresholds set at 80% sustained utilization to preempt overload failures.

###### _Anomaly scores in outputs_

Use drift detection models to score response quality deviations (e.g., semantic similarity to expected outputs), alerting on scores below 0.85.

###### _State consistency checks_

Count race condition incidents or synchronization failures, with immediate alerts for any nonzero occurrences in multiagent setups.

These metrics can be implemented using tools like Prometheus for collection and Grafana for visualization, integrated with AI-assisted anomaly detection (e.g., via Evidently AI) to predict failures before thresholds are breached. By setting context-aware thresholds—adjusted for workload peaks—teams reduce alert fatigue while ensuring timely intervention for internal issues like misconfigurations or emergent behaviors.

State management and consistency mechanisms help prevent failures caused by misaligned internal agent states or race conditions in multiagent workflows. Agents operating in distributed systems must maintain state synchronization to ensure that shared resources, databases, or operational dependencies are consistently updated and conflict-free. Techniques such as idempotent operations (where repeated actions produce the same result) and transactional state management (where operations are either fully completed or rolled back) provide additional layers of resilience.

Dependency isolation is another key measure for preventing internal failures. Agents often rely on plug-ins, third-party libraries, or external services, any of which could fail unpredictably. By isolating these dependencies—using technologies such as containerization or virtual environments—agents can limit the impact of failures in individual components. This isolation ensures that an unstable plug-in or an overloaded service does not compromise the entire agent system.

The risk of feedback loops and emergent behaviors also looms large in multiagent systems, where agents collaborate and communicate autonomously. Poorly designed communication protocols can result in unintended feedback loops, where one agent’s outputs trigger conflicting actions in another agent. To counteract this, systems must include coordination protocols that define clear rules for inter-agent communication and conflict resolution. Additionally, quorum-based decision making or voting mechanisms can help prevent single points of failure when agents need to reach consensus on critical decisions.

Regular validation and testing play a vital role in identifying and mitigating internal vulnerabilities before they manifest in production. Unit tests, integration tests, and stress tests should cover not only individual agent components but also their interactions across complex workflows. Simulation environments can serve as safe sandboxes to observe how agents behave under various edge cases, enabling developers to adjust their responses to failure scenarios.

Complementing traditional testing, chaos engineering practices offer a proactive way to stress-test agent system resilience and recovery mechanisms by intentionally introducing controlled failures in a simulated or production-like environment. Key practices include:

###### _Fault injection_

Simulate internal disruptions such as API latency spikes (e.g., adding 500millisecond delays), data corruption (e.g., injecting noisy inputs), or component crashes (e.g., killing a dependent plug-in) to observe how agents recover, using tools like Gremlin’s Chaos Engineering platform or Azure Chaos Studio.

###### _Game days and experiments_

Conduct structured “chaos experiments” where teams hypothesize failure modes (e.g., “What if state synchronization fails in a multiagent swarm?”), inject them gradually, and measure recovery time objectives (RTOs) and recovery point objectives (RPOs), aiming for subminute resolutions.

###### _AI-specific adaptations_

For agentic systems, focus on AI/ML pipeline failures like model drift or adversarial input floods, integrating AI to predict vulnerabilities (e.g., via the Harness AI-enhanced chaos tools) and automate experiment scaling.

###### _Blast radius control_

Limit experiments to isolated sandboxes initially, then expand to production with safeguards like automated rollbacks, ensuring lessons from failures (e.g., improved fallback strategies) are documented and applied.

By adopting chaos engineering—pioneered by Netflix’s Chaos Monkey and now extended to AI contexts—organizations uncover hidden weaknesses, such as feedback loops or dependency cascades, before they cause real outages, fostering a culture of resilience through empirical learning.

Furthermore, transparent reporting mechanisms ensure that internal failures are not silently ignored. Agents must be able to escalate errors, ambiguous states, or critical decision points to human operators when intervention is required. This transparency fosters a culture of accountability and prevents small internal errors from escalating into larger, system-wide failures.

Finally, organizations must establish postmortem analysis workflows to examine internal failures after they occur. These workflows should include detailed root cause analyses, corrective action plans, and documentation of lessons learned. The insights gained from postmortem reviews must feed back into the system design and deployment processes, closing the loop on continuous improvement.

In summary, internal failures in agent systems are inevitable, but their impact can be mitigated through thoughtful design, continuous monitoring, and proactive error

management. By implementing behavioral constraints, state consistency mechanisms, fallback strategies, dependency isolation, and robust validation frameworks, organizations can ensure that internal agent failures remain isolated, recoverable, and transparent. These protections not only enhance the resilience of individual agents but also safeguard the broader ecosystem of interconnected workflows they operate within.

###### **Conclusion**

We began by examining the unique risks posed by agentic systems, highlighting how autonomy, probabilistic reasoning, and misaligned goals introduce vulnerabilities that traditional software systems rarely face. The discussion then shifted to securing foundation models, emphasizing the importance of model selection, defensive techniques, red teaming, and fine-tuning to address adversarial threats and improve robustness.

We then proceeded to data security, underlining the importance of encryption, data provenance, integrity verification, and responsible handling of sensitive information. Data remains the lifeblood of agentic systems, and any compromise in its security can cascade into catastrophic failures or privacy violations.

Lastly, we turned our effort to securing agents themselves, addressing both external threats—such as adversarial attacks, supply chain risks, and social engineering—and internal failures, including misconfigurations, race conditions, and goal misalignment. Safeguards like role-based access controls, behavioral constraints, anomaly detection, and fallback mechanisms emerged as critical tools for preventing, detecting, and mitigating these vulnerabilities.

Securing agentic systems is not a onetime effort—it is an ongoing process of vigilance, iteration, and adaptation. As the threat landscape evolves and agent capabilities grow, organizations must remain proactive, continuously refining their safeguards, monitoring mechanisms, and governance practices.

In the end, building secure and resilient agent systems is not merely about mitigating risks—it’s about enabling agents to operate confidently in complex, real-world environments while upholding safety, fairness, and transparency. The lessons from this chapter provide a foundation for organizations to approach agent security as an integral part of their design and operational strategy, ensuring that the promise of agentic systems is realized without compromising safety, privacy, or trust.

### **CHAPTER 13 Human-Agent Collaboration**

As agentic systems weave into our workflows, success depends as much on how they collaborate with humans on raw capabilities. This chapter brings together the interaction-level mechanics (interfaces, uncertainty signals, handoffs) and the governance structures (oversight, compliance, trust calibration) that turn opaque assistants into dependable teammates.

Effective collaboration depends on calibrating autonomy: knowing when an agent should act on its own, when it should ask a question, and when it should defer entirely to a person. We’ll walk through strategies for progressive delegation—starting with simple drafts or suggestions and building toward greater independence as trust grows—and we’ll highlight how to repair that trust if mistakes happen.

###### **Roles and Autonomy**

This section explains how agentic systems shift from human-guided execution to autonomous operation—and how human roles evolve to match. As agent systems gain autonomy, one of the most important questions becomes: what role should the human play? The answer is not static. It shifts based on the task, the stakes, and— most critically—the level of trust between human and agent. This section explores how those roles evolve over time, how organizations can design for progressive delegation, and what it takes to align people, processes, and expectations as agents become more capable collaborators. We begin by tracing the arc from executor to governor, then examine the organizational dynamics that shape adoption and engagement.

###### **The Changing Role of Humans in Agent Systems**

As agent systems scale and mature within organizations, the role of the human collaborator evolves just as much as the technology itself. In early deployments, humans tend to act as executors, manually initiating agent tasks and closely supervising their outputs. Over time, as systems prove their reliability and establish trust, human roles shift toward reviewers—overseeing decisions at key checkpoints, particularly for high-stakes or regulated domains. This shift can be understood as a progression through four roles—executor, reviewer, collaborator, and governor. Each marks a shift in both the agent’s autonomy and the human’s responsibility. visualizes this arc, highlighting how the human role transforms alongside increasing system capability. The figure summarizes these roles and the interface needs associated with each.

Eventually, in mature workflows, humans become collaborators, sharing context, guiding priorities, and refining outputs alongside the agent in real time. The agent may draft, act, or even decide autonomously, but the human sets the high-level goals and intervenes when nuance, exception-handling, or moral judgment is required. In the most advanced deployments, humans transition into governors—defining policy boundaries, auditing systemic behavior, and overseeing how agent systems interact across teams and functions. We can see these responsibilities clearly in Table 13-1.

_Table 13-1. Roles, responsibilities, and interface needs in human-agent collaboration_

At JPMorganChase, for example, the internal COiN (Contract Intelligence) platform began with junior legal staff as executors, uploading contracts and reviewing every

clause extracted by the system. As COiN’s clause-extraction accuracy surpassed enterprise thresholds, experienced lawyers transitioned into reviewer roles, focusing only on nonstandard or edge-case documents. Senior counsels now serve as governors, defining extraction policies, auditing system behavior, and steering COiN’s expansion into new contract types. This structured delegation—from manual execution to policy governance—offers a clear example of how human roles evolve alongside autonomy.

Similarly, GitLab’s Security Bot began life in a classic executor mode—scanning merge requests with static analysis tools like static application security testing (SAST) and dynamic application security testing (DAST) and flagging potential vulnerabilities for engineers to manually address. Cases exceeding risk thresholds automatically escalate to designated security champions, who review and triage the bot’s findings. Their feedback is used to refine rules and lower false positives, gradually shifting the bot toward higher autonomy while maintaining human-in-the-loop oversight. Senior security leaders periodically audit both rules and escalation logs, performing the governor role to ensure escalation thresholds align with risk policy and compliance needs. This system illustrates how executor → reviewer → governor roles can coexist and flex as trust matures.

Each of these stages calls for different interface patterns and decision-making tools. Executors need clear instructions and tight feedback loops; reviewers require dashboards for exception management and audit visibility. Collaborators need interfaces for joint task planning and contextual annotation. Governors, by contrast, need system-wide observability, policy configuration, escalation logs, and tooling to validate alignment with compliance frameworks and human values.

Designing for human-agent collaboration means planning not only for the interactions of today, but also for the roles users—and their organizations—will grow into tomorrow.

###### **Aligning Stakeholders and Driving Adoption**

Even the most capable agentic systems can fail if they are not embraced by the people and teams they are designed to support. Too often, agents are introduced as technical upgrades but perceived as novelties or distractions—leading to poor adoption, passive resistance, or active workarounds. To avoid this, implementation must be as much a human change management effort as it is a software deployment.

Successful adoption begins with clear stakeholder alignment. Different teams may have very different expectations: engineers may focus on efficiency, legal teams on compliance, and end users on ease of use. If these expectations are not surfaced and harmonized early, agents risk being built for an imaginary “average” user who doesn’t exist. Misalignment breeds disillusionment.

The first step is to involve stakeholders early in the design process—not just as testers, but as co-creators. This includes defining clear goals: what specific outcomes should the agent improve? What decisions should it take on, and which should remain human-led? What would success—and failure—look like?

Crucially, success metrics must go beyond technical performance. An agent that completes tasks quickly but undermines trust or adds friction will not be adopted. Stakeholder buy-in depends on perceived usefulness, reliability, and alignment with existing workflows and values.

Implementing agentic systems is also an opportunity for broader organizational learning. When expectations diverge—between users and developers, or between what the agent can do and what stakeholders believe it should do—those moments can be used to clarify priorities, refine requirements, and recalibrate roles. Friction, if handled transparently, becomes fuel for iteration.

To support ongoing adoption, organizations should invest in training, feedback loops, and responsive support. Just as agents evolve, so should their onboarding materials and integration guides. Teams need spaces to voice concerns, propose improvements, and celebrate small wins as the agent grows into its role.

For example, ZoomInfo’s four-phase rollout of GitHub Copilot began with a small pilot of 50 engineers and only expanded to its full team of more than 400+ people once metrics (a 33% suggestion acceptance rate and 72% developer satisfaction) met carefully established thresholds—and qualitative feedback confirmed that Copilot suggestions were genuinely helpful. By tying each expansion to concrete trust signals, ZoomInfo transformed Copilot from a nice-to-have into a core productivity tool.

Ultimately, adoption is not a binary switch—it’s a journey of coevolution between humans and their agent teammates. Systems that succeed are those where stakeholders don’t just use the agent—they believe in its value and see it as an extension of their goals.

Bridging this gap is not optional. It’s the difference between agentic systems that quietly fade and those that truly transform how work gets done. With human roles defined and adoption strategies in place, we now turn to how collaboration itself scales—moving from individual assistants to team-wide and enterprise-level agents.

###### **Scaling Collaboration**

In this section, we examine how agents expand from individual assistants to team and enterprise collaborators—and what each stage demands of human and system design. As organizations adopt agents more broadly, their roles evolve from isolated assistants to collaborative participants embedded across teams, departments, and strategic workflows. Understanding how agent responsibilities scale—from personal tools to

organizational infrastructure—is essential for designing effective collaboration models, access controls, and governance structures.

At the smallest scope, agents serve individuals: helping manage calendars, summarize emails, or provide research support. These agents benefit from intimate context but have limited authority and minimal risk. Their success depends on understanding the preferences and working styles of a single user. Over time, individuals often delegate more responsibility to these agents, but oversight remains straightforward.

Team agents represent the next layer of complexity. They assist with shared knowledge management, project tracking, or meeting synthesis. These agents must navigate shared memory boundaries, respect interpersonal dynamics, and mediate across potentially conflicting expectations. They require more sophisticated context management and must surface uncertainties that might require group decision making rather than unilateral action.

We see this in Bank of America’s “Erica” assistant, which today handles over two billion customer requests and more than half of internal IT-help-desk tickets; by surfacing its confidence (e.g., “I’m 85% sure this answers your question”) and providing a clear handoff to a live agent whenever uncertainty rose above a defined threshold, Erica scaled from simple FAQs to trusted enterprise-wide service.

As we scale to division- or function-level agents—such as agents supporting finance, legal, or customer success—responsibilities expand dramatically. These agents interact with sensitive systems, touch multiple stakeholders, and influence performance at scale.

At this level, role-based access control (RBAC) becomes crucial. Agents must differentiate between public, internal, and restricted knowledge. They should have different privileges when acting on behalf of a VP than when assisting an intern. Clear delegation frameworks and logging are essential to ensure accountability.

At the highest level, enterprise-wide agents may coordinate workflows across departments, synthesize cross-functional data, or even advise on strategic decisions. These agents must operate within strong governance boundaries, subject to strict policies, regular audits, and often human sign-off for critical actions. They must be aware of inter-team dependencies, business rules, and organizational politics.

Critically, the design of these agents is not just a technical challenge—it’s a sociotechnical one. Agents must align with organizational culture, incentives, and workflows. Collaboration interfaces must make it easy for humans to review, approve, or modify agent outputs. Escalation pathways must scale with responsibility. And as agents span wider scopes, the cost of errors—and the need for well-defined trust boundaries— increases.

By recognizing the different scopes at which agents operate and designing accordingly, organizations can safely and effectively unlock their full potential—from individual productivity to systemic transformation.

###### **Agent Scope and Organizational Roles**

Not all agents are created equal—or rather, not all are created to serve the same _entity_ . As organizations scale their use of agentic systems, they naturally adopt agents that operate at different levels of abstraction and authority. Understanding and intentionally designing around these scopes is critical for safe, effective deployment. Agent deployments typically fall into one of five scopes, as shown in Table 13-2. As agents scale from personal assistants to organizational systems, their access scope, decision autonomy, and stakeholder impact increase. Each scope requires tailored design choices for permissions, oversight, and context management.

_Table 13-2. Agent scopes across organizational levels_

Each scope comes with different requirements for autonomy, oversight, data access, and trust calibration. For example, a personal agent can take small risks with limited scope, while an organizational agent must operate with rigorous guardrails, explainability, and auditing.

The first and most critical implication is the need for differentiated access control. As agents expand in scope, they must adhere to increasingly strict role-based access controls (RBAC) that align with their responsibilities and the sensitivity of the data they touch.

Personal agents may inherit permissions from the individual they assist, while functional or organizational agents require explicit privileges that reflect their designated role within enterprise systems. Designing this access architecture demands

coordination between IT, data governance teams, and agent developers to ensure that agents never exceed their intended scope.

These varying scopes also demand differentiated policies. Organizations should not apply a one-size-fits-all approach to autonomy, escalation, or logging. For instance, a personal agent might be permitted to send emails or schedule meetings autonomously, whereas a functional agent in finance may be required to route every action through a human-in-the-loop approval.

Organizational agents—those operating with the widest access—may require multiple layers of authorization or an internal governance board to review and approve behaviors and system updates. As agent scope increases from personal to organizational, both the autonomy level and associated risk rise. As is shown in Table 13-3, this progression demands increasingly robust governance—moving from lightweight user controls to enterprise-wide compliance, auditing, and oversight mechanisms.

_Table 13-3. Agent scope and risk_

Ultimately, defining agent scope is not just a technical architecture decision—it is a governance one. As agents become more essential to organizational workflows, their scope determines not only what they _can_ do, but what they _should_ do, and under whose watch. In the next section, we turn to the closely related question of how memory and context should be managed across these different scopes, and the trust, privacy, and continuity implications that arise when agents begin to remember not just for individuals—but for teams, departments, and the organization as a whole.

###### **Shared Memory and Context Boundaries**

As agents expand beyond individual use to support teams and organizations, how they manage memory becomes a critical design concern. Memory enables agents to personalize experiences, maintain context across sessions, and improve over time— but at larger scopes, it also introduces serious risks around privacy, misuse, and governance. Agents should never assume access to personal or sensitive data across

scopes without clear policy. Designing memory systems that respect these privacy boundaries—and make them auditable and enforceable—is key to ethical scalability.

Personal agents often store simple, user-specific context: preferences, past queries, inprogress tasks. But a team or departmental agent may need access to shared goals, conversations, or documents, and an org-level agent might build long-term memory of patterns across the business.

These broader memories are powerful—but also more sensitive. If a team agent recalls something shared in a private one-to-one chat, or a department agent surfaces confidential data across business units, the result could be a serious breach of trust or compliance.

To avoid this, memory must be scoped appropriately. Personal agents should default to isolated memory, only sharing data when explicitly allowed. Team and department agents should operate within shared but access-controlled memory spaces. Org-wide agents should work within policy-governed systems that enforce retention rules, logging, and auditability. In all cases, agents should be able to explain what they remember and why—and users should be able to inspect or delete that memory when needed.

Designers must also consider context flow. Should memory move upward (e.g., from a personal agent to a project agent)? Can agents query one another for context, or must they stay siloed? Clear boundaries are essential to prevent unintentional leaks or scope creep.

Just as important is making memory behavior transparent. Users should know what their agent remembers and be able to control it. That means surfacing memory visibly in the interface, giving people the ability to turn it off, and ensuring agents never make hidden assumptions based on stale or private data.

Ultimately, memory isn’t just a technical feature—it’s a source of power, trust, and risk. As agents operate at broader levels, we must treat memory as an asset that requires explicit governance, not an afterthought bolted onto stateful systems. Systems that manage memory well will feel coherent, helpful, and respectful. Systems that don’t will feel invasive, opaque, and unsafe.

As you’ve seen, designing agents for scopes from personal assistants to enterprisewide orchestrators requires tailoring autonomy, access controls, and interface patterns at each level. But remember: this is not a one-and-done exercise. Effective collaboration at scale is part of the same evolving journey we introduced at the start of this chapter—where human roles shift, trust deepens, and governance adapts alongside capability. Every new scope you unlock—from a project bot to a divisionlevel adviser—is another step along that arc of progressive delegation. With these patterns in hand, we’re ready to address the critical foundations of trust, governance, and compliance that underpin safe, ethical collaboration at every level.

###### **Trust, Governance, and Compliance**

Here we explore how to build and maintain trust, accountability, and oversight as agent autonomy grows—ensuring collaboration remains safe and aligned. As agents take on more critical roles in our workflows, trust and accountability become not just desirable—but essential. Technical performance alone is not enough. For agents to be effective partners, they must behave transparently, respect boundaries, and operate within well-defined governance frameworks. This section explores the foundations of trustworthy systems: how trust is built and calibrated over time, how responsibility and accountability are enforced, and how oversight and compliance mechanisms ensure agents act safely, ethically, and legally. From progressive delegation and auditing to escalation design and regulatory alignment, we examine what it takes to move from functional utility to dependable partnership.

###### **The Lifecycle of Trust**

Trust is not a binary state—it evolves. Users and employees don’t instantly trust agents just because they’re well designed or technically capable. Instead, trust is built gradually through consistent performance, transparent behavior, and clear boundaries. It can deepen with time—or erode quickly when an agent oversteps, fails silently, or behaves unpredictably.

A cautionary example is Klarna’s 2024 decision to replace roughly 700 customerservice roles with an AI chatbot: once empathy and nuanced judgment vanished, complaint volumes surged, forcing Klarna to rehire human agents by mid-2025 and underscoring that over-automation without robust human fallback can swiftly undermine trust.

Transparency plays a key role in trust calibration. Agents should proactively disclose their confidence levels, decision factors, and whether uncertainty was involved. Interfaces should make it clear _why_ the agent behaved a certain way—not just _what_ it did. At the personal level, trust grows as users see their agent remember preferences, follow instructions, and recover gracefully from mistakes. But at larger scopes—team, function, or organizational—trust becomes more complex. Now the agent represents not just one person, but a shared interest. Its actions may impact multiple users, trigger system-wide effects, or be interpreted as reflecting company policy. In these contexts, trust must be more deliberate and more distributed.

One key pattern is progressive delegation. Early in an agent’s lifecycle, it should act cautiously, deferring to humans for review or approval. As it proves reliable—and as users gain familiarity—its autonomy can expand. For example, a team agent might start by drafting status reports and eventually be trusted to send them. A finance agent might begin with read-only access and later be allowed to submit transactions

under supervision. Designing systems that support this staged growth of trust is essential for safe, scalable adoption.

To support that growth, agents should make trustworthiness visible. That means clear versioning, change logs, and audit trails. It means surfacing uncertainty, not hiding it. And it means giving users ways to override, intervene, or correct agent behavior without friction.

Organizations also need mechanisms for trust repair. When agents make mistakes— or when expectations shift—there should be a way to reset behavior, retrain, or restrict capabilities. Without a recovery path, even minor missteps can lead to lasting damage in confidence.

Ultimately, trust in agents mirrors trust in people: it must be earned, maintained, and rebuilt when broken. Designing for the lifecycle of trust—rather than treating it as a given—is one of the most important governance responsibilities for any system that seeks to integrate agents into meaningful human workflows. Yet trust alone is not enough. For agentic systems to truly transform work, they must be embraced—not merely tolerated—by the people they’re intended to support. That leap from reliability to real-world impact happens in the hands of users, teams, and leaders. But even strong trust must be anchored in systems of accountability. Trust may guide daily interactions, but governance must answer: what happens when things go wrong?

###### **Accountability Frameworks**

Accountability is critical for ethical agent design, ensuring that clear lines of responsibility exist for an agent’s actions, decisions, and consequences. Without accountability, failures—whether technical, ethical, or operational—can easily go unaddressed, eroding trust and leaving users or stakeholders without recourse. Establishing accountability requires both structural measures, such as oversight policies and escalation pathways, and technical measures, such as logging, traceability, and ethical audits.

Effective accountability frameworks ensure that failures are detected, analyzed, and addressed systematically, rather than being dismissed as unintended side effects of complex systems. These frameworks also define who is ultimately responsible—be it developers, system operators, or deploying organizations—when agent systems cause harm or make incorrect decisions.

To make accountability tangible, teams can adopt or adapt established frameworks— rather than inventing processes from scratch. Here are two readily available templates and resources:

- NIST AI Risk Management Framework (AI RMF)

- A voluntary, risk‐based approach published by the National Institute of Standards and Technology (NIST) that spans four core functions: govern, map, measure, and manage.

- Practitioners can download the AI RMF profiles and worksheets from NIST to map their own system’s risk levels, record mitigation strategies, and track progress over time.

- Co designed AI Impact Assessment Template

- Developed with input from AI practitioners and compliance experts, this template aligns with the EU AI Act, NIST AI RMF, and ISO 42001.

- It guides teams through documenting system purpose, stakeholder impacts, bias and fairness checks, and mitigation plans—usable both pre deployment and for ongoing governance.

Auditing plays a key role in maintaining accountability by offering structured assessments of agent behavior, system outputs, and decision pathways. Similarly, robust logging and traceability mechanisms ensure that every action an agent takes can be tracked, reviewed, and, if necessary, reversed or corrected.

Ethical audits are structured evaluations designed to identify ethical risks, unintended consequences, and potential harm arising from agent behavior. These audits go beyond technical testing to focus on the social, cultural, and organizational impacts of agent systems. Fairness must be treated as a first-class audit objective, not an afterthought. Audits should include checks for disparate impacts across demographic groups, feedback loops that might amplify bias, and the unintended consequences of optimizing only for accuracy or efficiency. An effective ethical audit typically involves:

###### _Evaluation of outputs_

Assessing whether an agent’s actions align with its intended goals and ethical guidelines

###### _Bias and fairness checks_

Identifying patterns of bias or unfair treatment in agent outputs

###### _Decision pathway analysis_

Reviewing how the agent arrives at its recommendations or decisions

###### _Stakeholder impact assessments_

Considering how the agent’s behavior affects different user groups or stakeholders

Behavioral assessments complement audits by observing how agents perform in realworld scenarios, especially under edge cases or ambiguous inputs. These assessments can identify unintended behaviors, such as agents making ethically questionable trade-offs or responding unpredictably to certain prompts.

Ethical audits and behavioral assessments should not be one-off activities—they must be ongoing, iterative processes. Agents evolve through updates, retraining, and exposure to new data, and their behavior must be reassessed regularly to ensure ongoing alignment with ethical standards.

Incorporating independent third-party audits can also add an additional layer of transparency and credibility. External experts can identify blind spots or risks that internal teams might overlook due to familiarity with the system.

Effective accountability relies on comprehensive logging and traceability systems that capture an agent’s decisions, actions, and contextual reasoning in detail. Logging serves as a recordkeeping mechanism, ensuring that every significant interaction or output is documented and can be reviewed later if needed. Well-implemented logging systems should include:

###### _Decision logs_

Records of why the agent made specific decisions, including inputs, intermediate reasoning steps, and outputs

###### _User interaction logs_

Details of user inputs and agent responses, with timestamps for clarity

###### _Error and failure logs_

Documentation of when and why an agent failed to complete a task or produced an unintended output

Traceability takes logging a step further by enabling auditors or developers to reconstruct an agent’s behavior in specific scenarios. This helps answer questions like the following:

- Why did the agent recommend this outcome?

- What data influenced this decision?

- Were there external factors (e.g., API failures, conflicting instructions) that impacted the result?

Traceability is especially crucial in high-stakes domains like healthcare, finance, or criminal justice, where the consequences of incorrect agent behavior can be severe.

Additionally, logs must be protected and managed responsibly. Unauthorized access to logs containing sensitive user data can introduce privacy risks. Encryption, access

controls, and data anonymization are essential safeguards for preventing misuse or breaches.

Logging systems must also be designed with clarity and usability in mind. It’s not enough for logs to exist—they must be interpretable by developers, auditors, and stakeholders. Clear documentation and visualization tools can help make traceability insights actionable.

###### **Escalation Design and Oversight**

Accountability doesn’t end with logs and audits—it must be backed by clear escalation mechanisms and human oversight structures that activate when agents encounter uncertainty, ambiguity, or ethical risk. As agents operate with increasing autonomy, organizations must answer a critical question: when—and how—should a human get involved?

Escalation design is the policy and infrastructure layer that ensures agents don’t act beyond their authority, especially in high-stakes or ambiguous situations. A welldesigned escalation framework defines clear thresholds for human intervention: specific decision types, risk levels, or confidence boundaries that require oversight. For example, a customer support agent might handle routine inquiries autonomously, escalate billing disputes to a human supervisor, and flag potential abuse cases to a trust and safety officer. Similarly, a procurement agent might be allowed to autoapprove purchases under $1,000 but require multiparty sign-off above that threshold.

These pathways must be encoded in both technical systems and organizational roles. Agents should be able to recognize when escalation is required—based on uncertainty, conflicting constraints, or explicit policies—and route tasks accordingly. Just as importantly, humans on the receiving end of escalations need context: what the agent attempted, why it escalated, and what information is needed to proceed.

Oversight isn’t just reactive. In well-governed systems, designated individuals or committees proactively monitor agent behavior, review logs, and refine escalation policies over time. These oversight roles may mirror existing structures—e.g., line managers, compliance leads—or they may require new positions such as AI operations analysts or agent governance officers. Oversight isn’t just about human-in-the-loop pathways; it includes the _guardrails_ —both policy and technical—that constrain agents to operate safely even in autonomous modes.

Escalation design also plays a key role in trust calibration. When users know that agents will defer at the right moments—and that humans can step in—they are more likely to rely on the system without over-trusting it. In contrast, systems without clear escalation logic tend to either frustrate users with false confidence or become paralyzed by uncertainty.

Finally, effective escalation design should support feedback loops. When humans resolve escalated cases, their decisions can be used to improve future agent behavior —whether through updated policies, retraining, or prompt tuning. Escalation isn’t a sign of failure; it’s a critical part of responsible autonomy.

In the next section, we’ll examine how agents scale across organizational scopes—and how oversight must evolve to match the complexity and risk of each context.

###### **Privacy and Regulatory Compliance**

As agent systems become integral to critical workflows across industries, they are increasingly subject to legal and regulatory scrutiny. Governments and international bodies are introducing AI-specific regulations to ensure these systems are deployed safely, ethically, and transparently. From data privacy laws to sector-specific compliance requirements, organizations building and deploying agents must navigate a complex and evolving regulatory landscape to mitigate legal risks and maintain public trust.

Compliance is not just about avoiding penalties. It’s about embedding ethical principles—such as fairness, transparency, accountability, and privacy—into the fabric of agent design and deployment. When implemented thoughtfully, compliance can serve as a foundation for more resilient, adaptable, and trustworthy systems. While regulatory requirements vary by region and industry, common themes emerge. Some of the most influential frameworks include:

###### _The EU AI Act_

A risk-based framework categorizing AI systems into levels of risk (e.g., minimal risk, high risk, unacceptable risk) with corresponding obligations for transparency, accountability, and human oversight.

###### _GDPR (General Data Protection Regulation)_

A cornerstone of global data privacy, requiring organizations to minimize data collection, ensure user consent, and provide clear pathways for data deletion and correction.

###### _CCPA (California Consumer Privacy Act)_

Offering data protection and transparency rights to California residents, emphasizing user consent and data access rights.

###### _HIPAA (Health Insurance Portability and Accountability Act)_

In healthcare, agents handling patient data must comply with strict privacy and security requirements.

###### _Industry-specific standards_

Including PCI DSS (Payment Card Industry Data Security Standard) for payment processing and SOX (Sarbanes-Oxley) for financial reporting integrity, each of which imposes additional constraints on agent behavior and data access.

Regulations are evolving rapidly, and what qualifies as compliant today may fall short tomorrow. Staying aligned requires ongoing investment in legal monitoring, architectural flexibility, and cross-functional collaboration. To make compliance sustainable, organizations should integrate it directly into their development pipelines, rather than treating it as a final gate. Key strategies include:

###### _Automated compliance gates_

As part of each build, run automated tests that scan for disallowed content (e.g., PII leakage), validate prompt testing against fairness benchmarks, and enforce data handling policies. Fail the build if any check trips.

###### _Policy as code libraries_

Leverage policy frameworks (e.g., Open Policy Agent) to codify your organization’s data use and privacy rules. Include policy tests alongside unit or integration tests, so that any policy drift is caught before deployment.

###### _Model cards and datasheets_

Generate a living “model card” as a build artifact—complete with lineage, training data statistics, known limitations, and intended use cases—and publish it to your internal model registry. Similarly, update a “datasheet” for each new training or fine tuning dataset, ensuring that every model version ships with a compliance ready bundle.

Many of the technical foundations of compliance align directly with best practices for privacy and security. These include: collecting only the data necessary for the task, stripping PII from datasets where possible, protecting data both at rest and in transit using strong encryption protocols, and restricting data access to only authorized users and systems.

Ensuring regulatory compliance isn’t just about meeting legal obligations—it’s about embedding compliance into every stage of the agent lifecycle, from design and training to deployment and long-term monitoring. This alignment requires a combination of technical safeguards, operational policies, and cultural commitments across the organization.

Let’s also remember that the regulatory environment is changing rapidly, and organizations must remain agile in the face of evolving regulations. This means tracking these changes, designing systems that can adapt quickly to new compliance mandates, and collaborating with legal and compliance experts throughout the agent lifecycle.

Security complements privacy, ensuring that even the data agents are allowed to access is shielded from breach, leakage, or tampering—an especially urgent concern as agents connect to sensitive back-office systems.

Trust, accountability, and regulatory alignment aren’t merely safety nets—they’re active ingredients in the partnership between humans and agents. We opened this chapter by arguing that collaboration must be designed as a journey, not a toggle switch, and the frameworks you’ve just explored close that loop: they give you the guardrails and recovery paths to move confidently from cautious pilots to full-fledged partnerships. As these governance mechanisms mature, they feed directly back into your design, keeping the cycle of adoption, learning, and progressive autonomy rolling forward until human-agent teams operate as seamless, trustworthy extensions of one another. We now look ahead to the future of human-agent teams—exploring how to sustain innovation, measure impact, and guide agentic systems toward truly human-centered outcomes.

###### **Conclusion: The Future of Human-Agent Teams**

Agent systems represent one of the most transformative technologies of our time, redefining how we interact with software, automate tasks, and solve complex problems across industries. From customer support chatbots and personal assistants to autonomous workflows and decision-making engines, agents are no longer experimental—they are becoming essential components of our digital infrastructure. This book has explored the multifaceted world of agent systems, diving deep into their design, orchestration, security, UX, and ethical considerations to provide a comprehensive guide for building effective and responsible agentic systems.

We began by laying the foundations of agent systems, exploring their promise, their distinctions from traditional software, and their unique strengths and challenges. From there, we examined the core principles of agent design, including skills, planning, memory, and learning from experience—all essential elements that enable agents to operate autonomously, adaptively, and effectively.

As we scaled from single-agent systems to multiagent coordination, we saw how agents can collaborate, negotiate, and distribute tasks to achieve goals that would be impossible for a single agent to handle alone. We also addressed the critical importance of measurement, validation, and production monitoring, emphasizing the need for robust evaluation frameworks and ongoing oversight to ensure reliable performance.

The book explored the security and resilience of agent systems, recognizing that agents can become attractive targets for malicious actors and vulnerable to unintended failures. We examined strategies for securing foundation models, protecting

sensitive data, and mitigating external threats and internal misconfigurations—all while balancing innovation with operational safety.

Finally, we addressed the ethical responsibilities inherent in building and deploying agent systems. As agents wield greater influence over our lives and decisions, the principles of oversight, transparency, accountability, fairness, and privacy become nonnegotiable. Ethical design isn’t a feature—it’s a fundamental requirement for ensuring that agent systems serve society responsibly and equitably.

Agent systems are not “set and forget” technologies—they must be continuously evaluated, improved, and aligned to evolving human needs. Agents must evolve alongside the challenges they are built to address, adapting to new data, emerging threats, and shifting societal expectations. The organizations that succeed will be those that prioritize agility, transparency, and a deep commitment to ethical principles.

At the same time, collaboration will be essential. Engineers, designers, ethicists, policymakers, and end users must work together to ensure that agent systems are not only powerful but also aligned with human values. The success of agent systems isn’t measured by their technical sophistication alone—it’s measured by their impact on individuals, organizations, and society as a whole.

As you move forward—whether as a developer, a team lead, an executive, or a policymaker—you are part of shaping the future of agentic systems. The tools, frameworks, and principles outlined in this book are starting points, not final answers, and we are all learning as we continue to move the field forward. Building agent systems is as much an organizational and cultural challenge as it is a technical one. Whether you’re just beginning or already deploying agent systems at scale, the path forward is iterative and collaborative. The most effective teams don’t leap to full automation—they build trust gradually, evaluate outcomes rigorously, and embed governance from the start. Here are four practical principles to guide your next steps:

###### _Experiment_

Pilot an agent in a low-risk domain.

###### _Measure_

Define success metrics before you start.

###### _Govern_

Establish oversight and logging early.

###### _Scale_

Iterate on trust and autonomy thresholds.

The rise of agent systems offers an extraordinary opportunity—a chance to amplify human potential, drive meaningful progress, and address challenges at scales previously unimaginable. But this future isn’t inevitable—it must be intentionally built, thoughtfully governed, and ethically guided. The choices we make today shape the digital future we leave for tomorrow. Building agents isn’t merely a professional obligation—it’s an opportunity to positively impact generations to come.

Let us create agentic systems that are not only smart but wise, not only efficient but just, and not only empowering but deeply committed to human flourishing.

### **Glossary**

###### **Activation function**

A mathematical function applied to a neuron’s input to determine the output, such as ReLU (rectified linear unit), Sigmoid, or Softmax.

###### **Agent**

An autonomous system that can perform tasks, make decisions, and interact with users or environments.

###### **Artificial intelligence (AI)**

The simulation of human intelligence in machines, including reasoning, learning, and problem-solving.

###### **Chatbot**

An AI system that interacts with users via natural language.

###### **Cold start problem**

The challenge of making predictions when little or no historical data is available.

###### **Context window**

The amount of text (measured in tokens) an LLM can process at once.

###### **Corpus**

A collection of text data used to train or fine-tune language models.

###### **Attention mechanism**

A technique in neural networks that allows models to focus on specific parts of input sequences, crucial for transformers.

###### **Backpropagation**

The algorithm used to train neural networks by adjusting weights based on error gradients.

###### **Beam search**

A decoding algorithm in sequence generation models that selects the most probable sequences.

###### **Bias**

Systematic errors in machine learning models that can lead to unfair outcomes.

###### **Decoder**

The component in transformer-based models that generates output sequences from encoded information.

###### **Dense vector**

A numerical representation of text in vector space, often used in embeddings.

###### **Domain adaptation**

The process of fine-tuning a model to perform better on a specific domain.

###### **Dropout**

A regularization technique that randomly deactivates neurons during training to prevent overfitting.

###### **Embedding**

A dense vector representation of words, sentences, or concepts in a continuous space.

###### **Encoder**

The component in transformer models that processes input text into a latent representation.

###### **Epoch**

One complete pass through a dataset during model training.

###### **Evaluation metrics**

Methods for assessing model performance, such as BLEU, ROUGE, or perplexity.

###### **Explainability**

The ability to understand and interpret how AI models make decisions.

###### **Hidden layer**

A layer in a neural network between the input and output layers where computation occurs.

###### **Hyperparameter**

A configurable parameter that affects model training, such as learning rate or batch size.

###### **Inference**

The process of using a trained model to generate predictions.

###### **Instruction tuning**

Fine-tuning models with task-specific instructions to improve performance.

###### **Intent recognition**

Detecting user intentions in natural language processing tasks.

###### **Joint embedding**

###### **Few-shot learning**

The ability of a model to generalize from a small number of examples.

###### **Fine-tuning**

The process of adapting a pretrained model to a specific task by further training on domain-specific data.

###### **Foundation model**

A large, pretrained neural network model that serves as a base for many downstream tasks.

###### **Generative AI**

AI models that generate new content, such as text, images, or music.

###### **Gradient descent**

An optimization algorithm used to minimize loss in machine learning models.

###### **Graph neural network (GNN)**

A type of neural network that processes graph-structured data.

###### **Hallucination**

When an AI model generates incorrect or nonsensical information.

A method where different modalities (text, images, audio) are mapped into the same vector space.

###### **KNN (K-nearest neighbors)**

A machine learning algorithm for classification and retrieval.

###### **Knowledge graph**

A structured representation of information with entities and relationships.

###### **Language model (LM)**

A statistical model that predicts the likelihood of word sequences.

###### **Latent space**

The abstract multidimensional space where data representations exist in neural networks.

###### **Logits**

The raw output of a neural network before applying a normalization function like Softmax.

###### **Long short-term memory (LSTM)**

A type of recurrent neural network (RNN) for handling sequential data.

###### **Masked language model (MLM)**

A pretraining technique where words in a sentence are randomly masked and predicted.

###### **Memory-augmented AI**

AI systems that maintain persistent knowledge beyond a single session.

###### **Meta-Agent Search (MAS)**

An automated process that explores, combines, and evaluates different agent architectures, components, and configurations to discover high-performing agentic systems.

###### **Meta-prompting**

Using structured prompts to guide an AI system’s behavior.

###### **Named entity recognition (NER)**

A technique for identifying entities like names, dates, and locations in text.

###### **Natural language processing (NLP)**

The field of AI focused on understanding and generating human language.

###### **Neural network (NN)**

A computational model inspired by the human brain, used in deep learning.

###### **Optimization**

The process of improving a model’s accuracy and efficiency.

###### **Overfitting**

When a model learns patterns that are too specific to the training data and fails to generalize.

###### **Parameter-efficient fine-tuning (PEFT)**

Techniques that adapt large models with minimal changes.

###### **Perplexity**

A measure of a language model’s uncertainty in predicting text.

###### **Prompt engineering**

The process of crafting inputs to maximize AI performance.

###### **Quantization**

Reducing a model’s precision to speed up inference.

###### **Query expansion**

Improving search results by adding related terms to a user’s query.

###### **Recurrent neural network (RNN)**

A type of neural network that processes sequential data.

###### **Reinforcement learning from human feedback (RLHF)**

A training technique where human preferences guide model behavior.

###### **Retrieval-augmented generation (RAG)**

A method where external knowledge is retrieved to enhance AI-generated responses.

###### **Scaling laws**

Principles governing how model performance improves with increased size and data.

###### **Self-attention**

A mechanism in transformers that determines the importance of different input tokens.

###### **Semantic search**

A search technique that retrieves relevant information based on meaning rather than exact words.

###### **Sequence-to-sequence (Seq2Seq)**

A model architecture used for translation and summarization tasks.

###### **Softmax**

A function that converts logits into probability distributions.

###### **Temperature**

A hyperparameter that controls randomness in AI-generated outputs.

###### **Tokenization**

The process of splitting text into units (tokens) for model input.

###### **Transformer**

A deep learning architecture that uses self-attention to process sequences efficiently.

###### **Unsupervised learning**

A type of machine learning where the model learns patterns without labeled data.

###### **Weight sharing**

A technique where the same model parameters are used across different parts of a network.

###### **Word embedding**

A method of representing words as dense vectors.

###### **XGBoost**

###### **User intent**

The goal behind a user’s query or request.

###### **Variational autoencoder (VAE)**

A neural network used for generative modeling.

###### **Vector database**

A specialized database optimized for storing and retrieving high-dimensional embeddings.

A gradient boosting algorithm commonly used for structured data.

###### **YAML (Yet Another Markup Language)**

A human-readable data format often used for configuration files.

###### **Zero-shot learning**

The ability of a model to perform tasks without explicit training examples.

