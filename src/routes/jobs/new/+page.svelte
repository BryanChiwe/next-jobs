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
            <label class="label" for="MaxAnnualCompensation">
                <span class="label-text">MaxAnnualCompensation</span>
            </label>
            <input type="MaxAnnualCompensation" name="MaxAnnualCompensation" placeholder="" class="input input-bordered w-full" required />
            {#if 'MaxAnnualCompensation' in formErrors}
            <label class="label" for="MaxAnnualCompensation">
                <span class="label-text-alt text-red-500">{formErrors['MaxAnnualCompensation'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="CompanyName">
                <span class="label-text">CompanyName</span>
            </label>
            <input type="CompanyName" name="CompanyName" placeholder="Zoo Negara" class="input input-bordered w-full" required />
            {#if 'CompanyName' in formErrors}
            <label class="label" for="CompanyName">
                <span class="label-text-alt text-red-500">{formErrors['CompanyName'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="JobLocation">
                <span class="label-text">JobLocation</span>
            </label>
            <input type="JobLocation" name="JobLocation" placeholder="bla bla" class="input input-bordered w-full" required />
            {#if 'JobLocation' in formErrors}
            <label class="label" for="JobLocation">
                <span class="label-text-alt text-red-500">{formErrors['JobLocation'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="Description">
                <span class="label-text">Description</span>
            </label>
            <input type="Description" name="Description" placeholder="Zoo Negara" class="input input-bordered w-full" required />
            {#if 'Description' in formErrors}
            <label class="label" for="Description">
                <span class="label-text-alt text-red-500">{formErrors['Description'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="Requirements">
                <span class="label-text">Requirements</span>
            </label>
            <input type="Requirements" name="Requirements" placeholder="hello" class="input input-bordered w-full" required />
            {#if 'Requirements' in formErrors}
            <label class="label" for="Requirements">
                <span class="label-text-alt text-red-500">{formErrors['Requirements'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="ApplicationInstructions">
                <span class="label-text">ApplicationInstructions</span>
            </label>
            <input type="ApplicationInstructions" name="ApplicationInstructions" placeholder="bye" class="input input-bordered w-full" required />
            {#if 'ApplicationInstructions' in formErrors}
            <label class="label" for="ApplicationInstructions">
                <span class="label-text-alt text-red-500">{formErrors['ApplicationInstructions'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Post Job</button>
        </div>
    </form>
</div>