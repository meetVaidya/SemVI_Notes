GANs are a type of neural network used in **unsupervised learning** to generate **new, realistic data** similar to existing data.

They involve two key components working against each other:
1. **Generator**
	- **Input**: Random noise
	- **Output**: Generates fake data that looks like real data
	- **Goal**: Fool the discriminator by making the data as realistic as possible.
2. **Discriminator**
	- **Input**: Real data and generated data
	- **Output**: Classifies whether the input data is real or fake
	- **Goal** Accurately distinguish real data from fake data


### GANs Explained
1. **Generative**
	- The **generator** learns a **probabilistic model** to create data samples.
	- Latent space sampling is the process of generating **random input vectors** (latent codes) from a simple probability distribution
	- Goal: Generate data that closely resembles the real data distribution.
	- **Example**: Creating realistic human faces from random noise.
2. **Adversarial**
	- The term "adversarial" refers to the **competition** between the generator and discriminator.
	- It's like a game where:
		- **Generator** tries to fool the discriminator by producing realistic data.
		- **Discriminator** tries to identify if the data is real or fake.
3. **Networks**
	- GANs use **deep neural networks** to analyze and generate data.
	- The networks help the generator and discriminator learn **complex patterns** and improve over time.
	- **Example**: Learning the texture, colour, and shape of human faces.

- **Latent Random Variable** → Random noise vector (input) is fed to the generator.
- **Generator** → The generator takes the noise and creates a synthetic sample.
- **Real World Images** → Real samples from the training dataset are also fed into the discriminator. 
- **Discriminator** → Discriminator tries to distinguish between real and fake samples.
- **Loss** → Discriminator outputs a score (real or fake) and sends feedback via loss to both generator and discriminator for improving their performance.