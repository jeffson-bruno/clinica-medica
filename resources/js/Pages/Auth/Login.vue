<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    usuario: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        
            <div class="w-full max-w-md">
                    <div v-if="status" class="mb-4 text-sm font-medium text-green-600">
                        {{ status }}
                    </div>

                    <form @submit.prevent="submit" class="bg-white p-6 rounded shadow">
                        <div>
                            <InputLabel for="usuario" value="Usuário" />
                            <TextInput 
                                id="usuario" 
                                type="text" 
                                v-model="form.usuario" 
                                required 
                                autofocus 
                                class="mt-1 block w-full"
                            />
                            <InputError :message="form.errors.usuario" class="mt-2" />
                        </div>

                        <div class="mt-4">
                            <InputLabel for="password" value="Senha" />
                            <TextInput
                                id="password"
                                type="password"
                                v-model="form.password"
                                required
                                autocomplete="current-password"
                                class="mt-1 block w-full"
                            />
                            <InputError class="mt-2" :message="form.errors.password" />
                        </div>
                    <div class="mt-4 block">
                        <label class="flex items-center">
                            <Checkbox name="remember" v-model:checked="form.remember" />
                            <span class="ms-2 text-sm text-gray-600"
                                >Remember me</span
                            >
                        </label>
                    </div>

                    <div class="mt-4 flex items-center justify-end">
                       <!--<Link
                            v-if="canResetPassword"
                            :href="route('password.request')"
                            class="rounded-md text-sm text-gray-600 underline hover:text-gray-900 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                        >
                            Forgot your password?
                        </Link>-->

                        <div class="mt-4 text-center">
                            <span class="text-sm text-gray-600">Criar Acesso</span>
                            <Link
                                href="/register"
                                class="ml-1 text-sm text-indigo-600 underline hover:text-indigo-900"
                            >
                                Clique aqui
                            </Link>
                        </div>


                        <PrimaryButton
                            class="ms-4"
                            :class="{ 'opacity-25': form.processing }"
                            :disabled="form.processing"
                        >
                            Log in
                        </PrimaryButton>
                    </div>
                </form>
            </div>
        
    </GuestLayout>
</template>
