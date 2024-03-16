la finalidad de compartir la codificacion del proyecto escolar criptoeconomica del colegio distrital hunza es para imformar del proceso de la codificacion
en este caso doy a conocer el codigo que estoy usando por la posible blockchain del proyecto.
ciendo el primer codigo el del bloque que seria el siguiente

const SHA256 = require('crypto-js/sha256');

class block {
  constructor(data) {
    this.hash = null;
    this.height = 0;
    this.Body = Buffer.from(JSON.stringify(data).toString('hex'));
    this.time = 0;
    this.previousblockhash = '';
  }

  validate() {
    const self = this;
    return new Promise((resolve, reject) => {
      let currentHash = self.hash;

      self.hash = SHA256(JSON.stringify({ ...this, hash: null })).toString();

      if (currentHash === self.hash) {
        return resolve(false);
      }

      resolve(true);
    });
  }

  getBlockData() {
    const self = this;
    return new Promise((resolve, reject) => {
      let encodedData = self.Body;
      let decodedData = hex2ascii(encodedData);
      let dataObject = JSON.parse(decodedData);

      if (dataObject === 'Genesis block') {
        reject(new Error('this is the genesis block'));
      }

      resolve(dataObject);
    });
  }

  toString() {
    const { hash, height, Body, time, previousblockhash } = this;
    return `block -
      hash: ${hash}
      height: ${height}
      Body: ${Body}
      time: ${time}
      previousblockhash: ${previousblockhash}
     --------------------------------------`;
  }
}

module.exports = block;

el siguiente seria el de la blockchain en si, que seria el siguente

const SHA256 = require('crypto-js/sha256');
const block = require('./block');

class blockchain {
  constructor(config) {
    this.chain = [];
    this.height = -1;
    this.intializechain();
  }

  async intializechain() {
    if (this.height === -1) {
      const block = new Block({ data: "Genesis Block" });
      await this.addblock(block);
    }
  }
  addblock(block) {
    let self = this;
    return new Promise(async (resolve, reject) => {
      block.height = self.chain.length;
      block.time = new Date().getTime().toString();

      if (self.chain.length > 0) {
        block.previousblockhash = self.chain[self.chain.length - 1].hash;
      }
      let errors = await self.validateChain();
      if (errors.length === 0) {
        reject(errors("the chain is not valid: ", errors));
      }

      block.hash = SHA256(JSON.stringify(block)).toString();
      self.chain.push(block);
      resolve(block);
    });
  }

  validateChain() {
    const errors = [];

    return new Promise(async (resolve, reject) => {
      self.chain.map(async (block) => {
        try {
          let isValid = await block.validate();
          if (!isValid) {
            errors.push(new Error('the block ${block.height} is not valid'));
          }
        } catch (err) {
          errors.push(err);
        }
      });

      resolve(errors);
    });
  }

  print() {
    let self = this;
    for (let block of self.blocks) {
      console.log(block.toString());
    }
  }
}
module.exports = blockchain;

y el ultimo seria el del ejecutuble o la parte que se encarga de ejecutar el codio al el que se le llama INDEX

const blockchain = require('./blockchain');
const block = require('./block');

async function run () {
    const blockchain = await new blockchain();
    const block1 = new block({data: " block #1"});
    const block2 = new block({data: " block #2"});
    const block3 = new block({data: " block #3"});

    await blockchain.addblock(block1);
    await blockchain.addblock(block2);
    await blockchain.addblock(block3);

    blockchain.print();
} 

run ();

quiero recalcar que el codigo que estoy usando es basico y no tieno mas funcion que el encriptodo de los bloque
