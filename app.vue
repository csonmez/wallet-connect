<script setup>
import AuthClient, { generateNonce } from '@walletconnect/auth-client'
import { Web3Modal } from '@web3modal/standalone'

const projectId = "f9bb30482237e84863ddb7353b3e8495"

const web3Modal = new Web3Modal({
  projectId,
  walletConnectVersion: 2,
  standaloneChains: ['eip155:1']
})

const authClient = await AuthClient.init({
  projectId,
  metadata: {
    name: 'Web3Lab',
    description: 'Web3Modal Laboratory',
    url: 'https://lab.web3modal.com',
    icons: ['https://lab.web3modal.com/favicon.ico']
  }
})

authClient.on('auth_response', ({ params }) => {
  web3Modal.closeModal()
})

const { uri } = await authClient.request({
  aud: 'https://yourapp.com/',
  domain: 'yourapp.com',
  chainId: 'eip155:1',
  type: 'eip4361',
  nonce: generateNonce(),
  statement: 'Sign in with wallet.'
})

if (uri) {
  await web3Modal.openModal({ uri })
}
</script>

<template>
  <div>
    deneme
  </div>
</template>
