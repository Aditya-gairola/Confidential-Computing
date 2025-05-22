# Confidential-Computing 🔐 

## What is Confidential computing
Much of the world’s most valuable data is sensitive and (rightly) protected. Companies don’t want proprietary data exposed; people and public organizations want to protect individual’s personal data. Protecting this privacy is essential, which is why sensitive data tends to stay within the walls of the organizations that collect it.

But not being able to collaborate on this data across these walls limits what this valuable data can do, from targeting the right person with ads that are actually relevant, to advancing medical research with real-world data.

Confidential computing is one of several technologies that aims to crack the conflict between data privacy and data utility. Confidential computing makes it possible to analyze data without having access to the actual data. And confidential computing provides hard proof that data remains private.

Confidential computing is a method to keep data private and encrypted while in use. Computation (like analyzing a set of data) happens in a separate, secure environment that only allows approved code in and approved results out. It lets you share insights without sharing data.

![image](https://github.com/user-attachments/assets/dcf74251-0c03-4226-a9e7-67fb8cdea04e)

``` With confidential computing, only encrypted data enters the trusted execution environment and only approved results leave. ```

This environment is usually a specific part of a computer’s hardware with strong security protections called a ```“trusted execution environment,”``` (TEE). A TEE can be a physically separate part of the computer, but it’s often completely encased in a protected area inside the computer’s main processor.

The TEE exists to create a space to run computations that is isolated and verifiable. Isolation means it’s kept completely separate from all other operations happening on the computer. Verification means you can tell exactly what programs are running in the TEE — so you can prove that the data itself stays private.

Encrypting stored data (”at rest”) and on the move (”in transit”) is common practice. But keeping the data encrypted while it’s in use (”in memory”) — and being able to prove it stays private through this entire journey — is a new advancement with confidential computing.

### How isolation and verification protect data during computation
Isolation and verification are the two most important security measures that make up confidential computing, and they work together to create a secure environment. Verification ensures that the computation is doing exactly what it is supposed to, and isolation ensures that that the computation is the only thing that accesses the data.

  - ### Isolation
      Isolation means that the rest of the computer can’t access any information happening inside the TEE, except through very specific and limited communication       channels. This is very different from normal computation processes.

    ![image](https://github.com/user-attachments/assets/0f8040d5-d2f6-4cd8-9776-7569e0412095)

      All modern computers provide basic process isolation to keep processes (like a data computation) separate when running on a chip like a CPU. However, this        isolation breaks down when the Operating System is compromised, which can happen fairly regularly.
  
      TEEs take isolation further by making it a separate system, not allowing any information flow unless it’s explicitly shared through dedicated communication       channels. This prevents other processes running on the same computer from learning information that was not explicitly shared. In a hardware-based TEE,           there are specific chip instructions that tell the chip which areas to isolate.
  
      TEE isolation can also be designed to keep information safe in memory. Information a computer or server is currently working on is kept in working memory,        or RAM. The RAM hardware is often made by a different manufacturer than the CPU, and is not part of the TEE. Regular memory isolation is not able to              guarantee that it prevents other processes from looking at or modifying the data held in memory.
  
      To provide robust isolation, the TEE uses encryption even for the information held in working memory. This is the same style of encryption you might be           familiar with for encrypting data at rest on the hard disc, but the fact that the TEE uses encryption to protect the data while it’s in use in working            memory is specific to confidential computing.

  - ### Verification
      Verification is the proof a TEE gives you to show that it’s secure. Also known as an “attestation”, it’s like a report of all the relevant information you 
      need to establish that it’s truly a secure and isolated environment.
      
      By design, it’s hard for the outside world to interact with a TEE, so the TEE itself has to provide evidence of two key things. First, it needs to prove 
      that it’s a real TEE, instead of something that’s pretending to be a TEE but isn’t really isolated. This is called “hardware identity”. Second, it needs to 
      provide information about exactly what code is running inside the TEE. This is called “hardware and software configuration”.

    ![image](https://github.com/user-attachments/assets/b6fb46e4-68b7-4b4d-88c8-2f9fc93bf9bd)

   - Hardware identity:
      - Answers the question “Who am I interacting with?”
      - Is it a Confidential computing-enabled chip from a known manufacturer, or is it rogue hardware?
     To prove that it’s really a TEE you are talking to, the TEE provides verification about what kind of TEE it is. The most important aspect of this           
     verification is usually a cryptographic signature provided by the hardware manufacturer, verifying that it is a genuine TEE that they made. The verification 
     (or “attestation”) and how the signature is incorporated is done in a way that it’s not possible to fake or reuse signatures.

   - Hardware and software configuration:
      - Answers the question “what is the status of the system I’m interacting with?”
      - Does it have isolation enabled, does it have a secure hardware configuration?
      - What software is loaded?
    To establish what code is running inside the TEE, the TEE creates a hash of the program in the TEE, called a “measurement”. This hash, or measurement, is a short value that uniquely identifies that exact program.
    
   You can use the measurement to make sure the code running in the TEE is what you intended: If you have a copy of the program, you can calculate its hash value, but a different program won’t be able to produce the same hash value. By comparing the measurement provided by the TEE to a hash that you calculated on your own, you can see if they match exactly and be sure that the TEE is running the exact same program.
    
  This specific verification process — proving the right code is running, and proving the TEE itself — is called remote attestation. “Remote” attestation means you can do it from anywhere: the signatures prevent a man-in-the-middle attack, allowing you to check the measurements of TEEs that are not local to you.

## Difference between confidential computing, a TEE and an enclave?

In conversation, people often use Trusted Execution Environment (TEE), enclave, and confidential computing interchangeably. Different manufacturers and vendors also sometimes use conflicting terminology. Here are the key differences:

  - TEE and enclave are broadly interchangeable terms. They typically refer to the specific, secure environment where confidential computing takes place and imply that the environment is hardware-based. A few rare exceptions of software-based “enclaves” exist, but they provide less robust security.
  
  - Confidential computing describes the entire act of computation using the TEEs the process of verifying the attestations reproducibly.

```A note on software-based “enclaves”```: While hardware TEEs are the most popular and secure technique for confidential computing, a few vendors also provide software-based solutions. They use software to create a virtual environment or machine that has security properties similar to a TEE within that virtual layer.

Some consider this approach less secure because while it can provide the same protections within the virtual layer, that virtual layer sits on top of another layer that has its own security vulnerabilities. Someone operating or hacking into that base layer could access or modify information. Gaining the same level of control over a hardware enclave would require someone to physically access and manipulate the actual hardware, which is more challenging and can be mitigated with physical security.

## Confidential computing use:

You’ve likely used confidential computing without knowing it — TEEs are in most mobile phones. Personal devices like phones and laptops were the first place confidential computing saw widespread use. Because they contain lots of sensitive information, they’re prime targets for hacking, malware and other attacks.

Chip manufacturers wanted to create secure places to store and process information that would remain secure even if a device got hacked. Some of the early uses include keeping passwords and similar secrets safe, or running software to check that a device was authorized to use a specific program or access a piece of media.

Intel introduced Software Guard eXtensions (SGX) in 2016, which brought about a major shift in how TEEs could be used. Unlike most earlier TEEs, SGX could run on servers on a large scale, and it enabled remote attestation — making confidential computing “in the cloud” feasible. This set off a small explosion of research and interest into this new way of approaching computational security.

Other hardware vendors and instruction set families like AMD, ARM, IBM, RISC-V, and Nvidia have since followed suit and released or announced development of TEE technology that is suitable for confidential computing.

Today, some of the most promising applications of confidential computing are designed to make the best use of sensitive data while protecting it. The messenger app Signal, for example, uses confidential computing to help you find which of your contacts already use the app — without having to give Signal access to your address book. Edgeless Systems built a confidential computing solution for training AI models that keeps sensitive data encrypted during the entire model training pipeline.




  
