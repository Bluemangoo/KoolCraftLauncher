<template>
  <div class="w-full h-full flex flex-col gap-3">
    <div v-for="account in accountStore.accounts"
         :key="account.namespace + account.uuid"
         class="px-0 flex h-11 w-full rounded-1 overflow-clip"
    >
      <span>
        <account-avatar :size="44"
                        :account="account"
                        :class="{
                            'rounded-tr-1': !accountStore.isCurrentAccount(account),
                            'rounded-br-1': !accountStore.isCurrentAccount(account),
                        }"
        />
      </span>
      <span class="w-full">
        <v-btn size="large"
               :variant="accountStore.isCurrentAccount(account) ? 'tonal' : 'plain'"
               class="pt-0 w-full custom-btn"
               :rounded="false"
               :active="accountStore.isCurrentAccount(account)"
               @click="accountStore.currentAccount = account">
          <div class="w-full flex">
            <span class="text-transform-none text-left text-body-1 ml--3">
              {{ account.name }}
            </span>
            <v-spacer />
            <v-chip class="mr--3"
                    size="small"
                    :text="t(`account.type-short.${ accountStore.getAccountTypeLabel(account) }`)"
            />
          </div>
        </v-btn>
      </span>
    </div>
    <div>
      <div class="h-16"></div>
    </div>
    <div class="pos-fixed bottom-4 right-6">
      <v-btn size="large"
             variant="elevated"
             :icon="mdiPlus"
             @click="router.push('/account/add')"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { mdiPlus } from "@mdi/js";
import { useAccountStore } from "@/data/account/account";

const { t } = useI18n();
const router = useRouter();
const accountStore = useAccountStore();
</script>