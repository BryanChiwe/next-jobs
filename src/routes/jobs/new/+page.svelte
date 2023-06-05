<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
	import { getUserId } from '../../../utils/auth';
    let formErrors = {};

    function postCreateJob() {
        goto('/');
    }

    async function createJob(evt) {
        evt.preventDefault();

        const userID = getUserId();

        const jobData = {
        user: userID,
        title: evt.target['title'].value,
        minAnnualCompensation: evt.target['minAnnualCompensation'].value,
        maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
        employer: evt.target['employer'].value,
        location: evt.target['location'].value,
        description: evt.target['description'].value,
        requirements: evt.target['requirements'].value,
        applicationInstructions: evt.target['applicationInstructions'].value
       };

        const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
          method: 'POST',
          headers: {
              'Content-Type': 'application/json'
          },
          body: JSON.stringify(jobData)
        });

         if (resp.status == 200) {
          postCreateJob();
         } else {
          const res = await resp.json;
          formErrors = res.data
         }
    }
</script>



<div class="text-center text-xl mt-5">Post a Job Below</div>

<div class="flex justify-center items-center mt-8">
    <form on:submit={createJob} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">jobtitle</span>
            </label>
            <input type="text" name="title" placeholder="Orang Utan" class="input input-bordered w-full" />
            {#if 'title' in formErrors}
            <label class="label" for="title">
                <span class="label-text-alt text-red-500">{formErrors['title'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="minAnnualCompensation">
                <span class="label-text">minAnnualCompensation</span>
            </label>
            <input type="minAnnualCompensation" name="minAnnualCompensation" placeholder="john@example.com" class="input input-bordered w-full" required />
            {#if 'minAnnualCompensation' in formErrors}
            <label class="label" for="minAnnualCompensation">
                <span class="label-text-alt text-red-500">{formErrors['minAnnualCompensation'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="maxAnnualCompensation">
                <span class="label-text">MaxAnnualCompensation</span>
            </label>
            <input type="maxAnnualCompensation" name="maxAnnualCompensation" placeholder="" class="input input-bordered w-full" required />
            {#if 'maxAnnualCompensation' in formErrors}
            <label class="label" for="maxAnnualCompensation">
                <span class="label-text-alt text-red-500">{formErrors['maxAnnualCompensation'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="employer">
                <span class="label-text">CompanyName</span>
            </label>
            <input type="employer" name="employer" placeholder="Zoo Negara" class="input input-bordered w-full" required />
            {#if 'employer' in formErrors}
            <label class="label" for="employer">
                <span class="label-text-alt text-red-500">{formErrors['employer'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="location">
                <span class="label-text">JobLocation</span>
            </label>
            <input type="location" name="location" placeholder="bla bla" class="input input-bordered w-full" required />
            {#if 'location' in formErrors}
            <label class="label" for="location">
                <span class="label-text-alt text-red-500">{formErrors['location'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="description">
                <span class="label-text">Description</span>
            </label>
            <input type="description" name="description" placeholder="Zoo Negara" class="input input-bordered w-full" required />
            {#if 'description' in formErrors}
            <label class="label" for="description">
                <span class="label-text-alt text-red-500">{formErrors['description'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="requirements">
                <span class="label-text">Requirements</span>
            </label>
            <input type="requirements" name="requirements" placeholder="hello" class="input input-bordered w-full" required />
            {#if 'requirements' in formErrors}
            <label class="label" for="requirements">
                <span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="applicationInstructions">
                <span class="label-text">ApplicationInstructions</span>
            </label>
            <input type="applicationInstructions" name="applicationInstructions" placeholder="bye" class="input input-bordered w-full" required />
            {#if 'applicationInstructions' in formErrors}
            <label class="label" for="applicationInstructions">
                <span class="label-text-alt text-red-500">{formErrors['applicationInstructions'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Post Job</button>
        </div>
    </form>
</div>